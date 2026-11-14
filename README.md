# DevTool

A native desktop app for managing git worktrees on macOS, with built-in device tools for iOS and Android development (simulators/emulators, logs, network, storage, and more).

This repository is the **download and support home** for DevTool. It does not contain the application's source code.

## Download

Grab the latest `.dmg` from [Releases](../../releases/latest).

```bash
# or, via Homebrew
brew install --cask j1king/tap/devtool
```

Open the `.dmg` and drag DevTool to Applications. On first launch, macOS Gatekeeper may ask you to confirm you trust the developer — this is expected for apps outside the App Store.

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
