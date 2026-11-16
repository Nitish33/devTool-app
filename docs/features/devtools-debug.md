# Dev tools: debug and performance

Find out what the app is doing, and why it is slow.

[← All features](../../README.md#features)

**On this page:** [Network](#network) · [WebView](#webview) · [UI tree](#ui-tree) · [Logs and console](#logs-and-console) · [Timers and listeners](#timers-and-listeners) · [React profiling](#react-profiling) · [Performance](#performance) · [Image audit](#image-audit)

## Network

Every request the app makes, like Chrome's Network panel.

- **Request list** with name, status, size, time, and a Mock and Throttle column; filter and clear
- **Details:** headers (request and response), query string, payload, preview, response and timing
- **Call stack** for each request, with the line opened in your editor
- **Copy as cURL**
- **Mock responses:** answer a request with your own status, delay, headers and body; match by method and URL; turn rules on and off; start one from a real response
- **Mock rules dialog** to manage all your rules in one place
- **Throttle everything** with a random delay, and **throttle one request** with its own range
- **Request editor window** for a request's mock and throttle together
- **See what happened:** which requests were held, for how long, or answered by a mock
- **Filter by kind** like Chrome's Network panel: Fetch/XHR, Doc, CSS, JS, Font, Img, Media, WS and Other (⌘-click to pick several), plus **Errors** and **Mocked**, each with a count
- **Reconnects on its own** and puts your mocks and throttles back
- **Older React Native** (before 0.83), which cannot report its requests to a debugger: they are noted from the app's JavaScript instead (requests made through `fetch` and XHR; images loaded by the native side are not seen)

![The Network tool with a request open](images/network.webp)

![The request editor with a mock response](images/network-mock.webp)

![The throttle setting with a delay range](images/network-throttle.webp)

## WebView

Debug a WebView inside the app, like Safari's inspector or Chrome's remote debugging, on an iOS simulator or an Android emulator or phone.

- **Console:** what the page logs and throws, and a prompt that runs JavaScript in the page
- **Network:** the same list as the Network tool, with the same kind filters, details, **mocks and throttles** (for the page's `fetch` and XHR)
- **Messages:** every message between the app and the page (`ReactNativeWebView.postMessage` and what the app sends in) as a stack of cards with the JSON opened up, and a way to send one either way
- **Window:** the page's `window` object as a tree you can open, edit and add to, and scripts you keep, run now, or run on every load
- **Application:** cookies (add, edit, delete), local and session storage, IndexedDB and caches
- **History:** back, forward, reload, go to an address, the pages visited, and on Android the WebView's back stack
- **Elements:** an element inspector: the page's tree, **pick an element by touching the page on the device**, a highlight with margin, padding and size, its styles, computed styles, box and attributes (editable), and search by text, id, class or CSS selector
- The app's WebView must be inspectable (`webviewDebuggingEnabled` in react-native-webview). A page allows one inspector at a time

![The WebView Network tab, with a response opened as a JSON tree](images/webview-network.webp)

![The WebView History tab with the pages seen since attaching](images/webview-history.webp)

![The WebView Elements tab with the element picked on the device highlighted](images/webview-elements.webp)

## UI tree

The views of the app by **test ID, label and text**, with how much of each is in view. Choose **On screen**, **Everything** (including what is off screen in a long list) or **No test ID** (what can be pressed but cannot be asked for by name).

- A way to **scroll to** a view and to **tap** it, which is what an agent does: the view is brought into view first, and a tap only goes through when a touch would reach it
- Type into a view, swipe, and press Home
- Updates itself as you use the app
- See [adding test IDs](test-ids.md) and [AI agents](agent.md)

## Logs and console

Native logs and the JavaScript console in one tool.

- **Two sources:** the device's native logs, and the app's JS console
- **Level menu** (errors, warnings and so on) and a **columns menu**
- **Filter** text (⌘F), and filter by **app name**
- **Pause or stop** the stream; **clear**; follow the latest message
- **Copy** the visible lines, or **copy for AI** with a prompt that points to a saved file
- **Live indicator** shows whether lines are coming in

![The Logs and console tool with a level menu open](images/logs.webp)

## Timers and listeners

Find leaks and runaway work.

- **Everything the app started and hasn't ended:** timers and event listeners
- **Where each was started** in your code, and which component started the most
- **What to look at:** places with many still running, or listeners added and never removed
- **How they ended:** running, ended, cleared or expired
- **Chain origin:** for something that restarts itself (a loop or a poll), the code that began it
- **Filters:** hide the ended ones, or show only places worth a look; **clear the ended**

![The Timers and listeners tool with places to look at](images/timers.webp)

## React profiling

Which components render, how often, how long, and why.

- **Record** and stop, then explore
- **Components view:** renders, wasted renders, self time, average and slowest, with the reasons shown as colored bars
- **Flame graph:** the component tree for a commit, wider for longer
- **Ranked chart** of time spent in each component
- **Commit chart:** every commit as a bar, with arrows to step through
- **Why did this render?** changed props and hooks, with before and after; flags **a new object with the same content**
- **Named hooks**, and **open the source** at the line where a hook is called
- **Avoidable renders**, and a hint when a prop changes on nearly every render
- **Hide library components**, and filter by name
- **Save and load profiles**, and **copy for AI** with a prompt that points to the recording

![The profiler with the flame graph](images/render-profiler.webp)

![Component details with changed props and hooks](images/render-details.webp)

## Performance

Where the app's JavaScript spends time and memory.

- **CPU profile:** record for a while, then see the slowest functions, a call tree, and your code only
- **Memory:** the heap over time, snapshots, and compare two to see **only what grew**; free unused memory first
- **Startup:** how long each module took from launch to first screen, by package; **measure a new start**
- **Bundle:** the size of each package in your bundle, built as it would ship
- **Open in the editor** from any function or module

![The Performance tool with a CPU profile](images/performance.webp)

![The Memory view comparing two snapshots](images/performance-memory.webp)

## Image audit

Find images that waste memory and data.

- **Audit this screen:** lists every image on screen with its original size, the size it is shown at, and what that costs
- **Flags:** oversized, blurry (upscaled), big in memory, big file, repeated downloads, not cacheable, wrong format, off screen, hidden
- **Savings:** memory and download size each fix would save, and a total
- **Sizes and cache headers** are read from the image's server when the network log missed them
- **Sort** by wasted memory, file size and more; **copy an image's address**

![The Image audit results with flagged images](images/image-audit.webp)
