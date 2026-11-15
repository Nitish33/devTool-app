# Requirements and limits

What DevTool needs to do its job.

[← All features](../../README.md#features)

## What you need

Before you start.

- **macOS 10.15 or later**, and **Git** installed
- **iOS simulators:** Xcode
- **Android emulators and phones:** `adb` from the Android SDK platform-tools
- **React Native tools** (navigation, Redux, storage, network and so on): a development build with Metro running and the app connected. They change nothing in your project
- **Smaller recordings:** ffmpeg, if you have it; without it the original is kept

## Good to know

Things that behave differently on purpose.

- **Data snapshots on Android** work for debug builds only, because they read the app's private files
- **iOS keychain** isn't part of an app's data, so snapshots don't include it
- **iOS push notifications** reach simulators only, and images added by a notification extension don't show there
- **Image audit** memory sizes are estimates
- **Spotlight quick links** show only in an installed, signed build
