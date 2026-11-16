# Flows and cassettes: tests that always see the same API

UI tests break when the backend changes underneath them. DevTool fixes that by **recording the app's API once** and **replaying it** every time a test runs, so the same taps always meet the same data. The recording is a **cassette**; the steps are a **flow**. Neither needs an AI agent to run.

```
record once (you, or an agent)      run as often as you like
─────────────────────────────       ──────────────────────────────────
use the app, real server            DevTool --run checkout.flow.json
   ↓                                   ↓ replays checkout.cassette.json
checkout.cassette.json  (the API)       ↓ does the steps, waits for the app
checkout.flow.json      (the steps)     ↓ checks what the flow expects
                                        exit code 0 (passed) or 1 (failed)
```

## Record once

Ask your agent (it needs the [MCP server](agent.md)) to record the use case, or call the tools yourself:

1. `cassette_record_start` with a `name`, and `saveTo` (a path inside your project, so the files can be committed).
2. Do the use case on the simulator with the real server reachable: tap through it with the `ui_*` tools, or by hand.
3. `cassette_record_stop` saves **`<name>.cassette.json`** and, from the agent's actions, **`<name>.flow.json`**, and returns a **review**.

**Read the review.** It is where a cassette goes wrong: which endpoints answered differently from call to call (they are replayed in order), which values were treated as changing every run, tokens that were made long-lived, what could not be kept (images, bodies too large), and other hosts that were not recorded and so reach the real network.

## Run it, with no agent

From the app: the **Agent** tool has a **Flows** card that lists the flows in `~/.devtool/flows` and `~/.devtool/cassettes`, newest first. **Run** a flow there and see the pass or fail and the report in place; the folder icon opens the folder. From a terminal:

```
DevTool --run checkout.flow.json            # DevTool must be running, with a simulator or emulator
DevTool --run checkout.flow.json --device "iPhone 16 Pro" --strict all
```

Exit code: **0** the flow passed, **1** it failed, **2** it could not be run. The report lists every step with the time it took. When a step fails you also get the screen as it was and a screenshot. Agents can run the same thing with `flow_run`. The run appears in the Agent tool as a session.

What DevTool does for you while it runs:

- **Starts from the same place.** The app is reloaded first (`"reload": false` to skip), and the cassette starts from its first answer.
- **Waits for the app.** A step that taps or types waits until React has not changed the screen for 150 ms (a touch that comes while the app is still rendering is lost), tries again for up to 8 seconds if the element is not ready, and after it waits for the requests it started to finish. You do not write waits.
- **Checks what it typed.** After typing into a field it reads the field back, and types again if the keyboard dropped or changed a key.
- **Judges the API.** A request the cassette has no answer for is **refused and fails the run**, with the closest recorded request so you can see what differs. Nothing reaches the real server quietly.

## The flow file

```json
{
  "format": "devtool-flow/1",
  "name": "browse users",
  "cassette": "users.cassette.json",
  "steps": [
    { "do": "tap", "testID": "menu-api" },
    { "expect": "request", "method": "GET", "url": "/users", "status": 200 },
    { "expect": "visible", "text": "Leanne Graham" },
    { "do": "tap", "testID": "api-reload" },
    { "expect": "request", "url": "/users", "atLeast": 2 },
    { "expect": "no_console_errors" }
  ]
}
```

| Step | Fields |
|---|---|
| `do: tap` | `testID` (or `text`, `label`), `index` |
| `do: type` | `text`, `testID` of the field (or the focused one), `clear`, `submit` |
| `do: scroll` | `to` (`top`, `bottom`, `up`, `down`) or a `testID` |
| `do: swipe` | `direction`, optionally an element |
| `do: press` | `button`: `home`, `lock`, `back`, `recents` |
| `do: open_link` · `reload` · `wait` | `url` · none · `ms` (avoid: steps wait by themselves) |
| `do: tool` | `tool` and `args`: any other tool |
| `expect: visible` · `gone` · `enabled` | an element |
| `expect: text` | an element, and `equals` or `contains` |
| `expect: request` | `url` (a part of it), `method`, `status`, `count` (exactly) or `atLeast` |
| `expect: no_unmatched` · `no_console_errors` · `no_failed_requests` | none |

Any step can have `timeoutMs` (default 8000) and `optional: true` (it may fail without failing the run). At the top: `cassette` (a name, or a path beside the flow), `strict`, `reload`, `settle`, `ignoreQuery`, `ignoreBody`, `allowUnmatched`, `failOnConsoleError`.

## How a request is matched

On **method, path, query and body**, never the host (so a cassette recorded against staging replays anywhere). Left out of the comparison, because they change every run: UUIDs, timestamps, `timestamp`, `ts`, `nonce`, `requestId`, `traceId` and the like. Add your own with `ignoreQuery` and `ignoreBody` (names, at any depth). GraphQL works because the body is compared: two operations to one URL are two requests.

The same request made again gets the **next recorded answer** (the second `GET /cart` gets the second answer), and the last answer once they run out.

`strict` says what happens to a request that was never recorded: **`hosts`** (default) refuses it when its host was recorded; **`all`** refuses every one; **`off`** lets it through.

## Replay by hand

`cassette_replay` and `cassette_replay_stop` do the replay part alone, for an agent or for you to try the app against the recording. While one is on, the **Agent tool shows a "Replaying" card** with how many requests were answered and a **Stop replay** button, so the app showing recorded data is never a mystery. Your own `network_mock` rules still win over the cassette: replay everything, and force one endpoint to fail.

## Limits

- **Requests made from JavaScript** (`fetch`, axios, XMLHttpRequest). A native SDK's own calls are not covered; the review says so.
- A **development build** with Metro, on a simulator or emulator, with DevTool running. It is not a release-build or headless runner.
- Recorded responses **go stale** as the real API changes. Record again when it does; the review and the refused-request report tell you where.
- **Tokens**: a JWT or `expires_at` in a recorded response is moved ten years on, so an old login does not log the replay out. Time itself is not frozen: an app that checks the device clock against a server date can still disagree.
- Responses larger than 400 kB and binary ones are not kept.
