# DevTool

A native desktop app for managing git worktrees on macOS, with built-in device tools for iOS and Android development (simulators/emulators, logs, network, storage, and more).

This repository is the **download and support home** for DevTool. It does not contain the application's source code.

## Download

Grab the latest `.dmg` from [Releases](../../releases/latest).

Open the `.dmg` and drag DevTool to Applications.

### First launch (unsigned-for-distribution builds)

This build isn't notarized by Apple yet, so macOS will refuse to open it and say it "could not verify DevTool is free of malware" — and **the usual fixes (double-click, right-click → Open, or Settings → Privacy & Security → Open Anyway) will not work for this particular warning.** That only works for a different, less strict category of unsigned app.

To open it anyway, run this once in Terminal, then launch DevTool normally:

```bash
xattr -d com.apple.quarantine /Applications/DevTool.app
```

If that doesn't clear it:

```bash
xattr -cr /Applications/DevTool.app
```

We know this is a rough first step and are working on a properly notarized build, which won't need this.

### Requirements

- macOS 10.15 or later
- Xcode (for iOS simulators) and/or Android Studio (for emulators), if you plan to use the device tools

## Reporting issues

Found a bug or have a feature request? Please [open an issue](../../issues/new/choose) — use the bug report or feature request template so we have what we need to help.

Before filing, please check [existing issues](../../issues) first.

## What's collected

DevTool sends anonymous, aggregate usage statistics (which features are used, app and OS version) and crash reports, to help us fix problems and prioritize what to build next. No file paths, repository names, branch names, credentials, or file contents are ever collected. See [NOTICE.md](NOTICE.md) for details.

## License

DevTool is proprietary, closed-source software. See [LICENSE.md](LICENSE.md) for the terms under which it is distributed. The source code is not published, and reverse engineering is prohibited except where applicable law gives you that right despite this restriction.

## Support

For a security issue, please use GitHub's private [report a vulnerability](../../security/advisories/new) form rather than a public issue.
