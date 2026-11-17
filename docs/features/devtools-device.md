# Dev tools: device

Change the device and the app's data without leaving the window.

[← All features](../../README.md#features)

**On this page:** [Device settings](#device-settings) · [Location](#location) · [App data](#app-data) · [Cookies and local storage](#cookies-and-local-storage) · [Deep links](#deep-links) · [Push notifications](#push-notifications) · [Design tools](#design-tools) · [Design overlay](#design-overlay) · [Builds](#builds) · [Data snapshots](#data-snapshots) · [Recording and screenshots](#recording-and-screenshots) · [Permissions](#permissions)

## Device settings

Set up the device the way a test needs.

- **Theme:** light or dark
- **Text size** and **display size**, including the accessibility sizes
- **Navigation mode:** gestures or 3 buttons (Android)
- **Date and time:** set by hand, or automatic; 24-hour clock
- **Reset** back to what the device had

![The Device tool with theme, text size and clock](images/device-settings.webp)

## Location

Put the device anywhere.

- **Mock the location** with latitude and longitude; paste "lat, long" from a map
- **Save places by name** and move the device with one click
- **Stop mocking** to return to the simulator's own location

![The Location section with saved places](images/location.webp)

## App data

Start from a clean slate, quickly.

- **Clear the cache**
- **Clear all data:** starts the app as if just installed (data, settings, cache and permissions)
- **Reset the keychain** too, so signed-in sessions are gone
- **Open the app afterwards**

![The App data section with the clear options](images/app-data.webp)

## Cookies and local storage

Look at and change what the app saved.

- **Cookies:** view, filter, copy, edit, add and delete; domain, path, expiry, Secure, HttpOnly and SameSite
- **AsyncStorage:** view, filter, copy, edit, add and delete; **format or minify** JSON values
- **Clear all** with a confirmation
- **Restart the app** after a change if you want it to read the new values

![The cookies and AsyncStorage cards](images/cookies-storage.webp)

## Deep links

Open the app's links on the device.

- **Save links** with a name and an app, per platform
- **Open** one with a click, **edit** or **delete** it

![The Deep links tool with saved links](images/device-deep-links.webp)

## Push notifications

Send a push as if it came from your server.

- **Templates:** alert, title, with a link, silent, data only, badge, with an image
- **Edit the payload** as JSON, with validation (including APNs limits)
- **Save payloads** by name per platform
- **iOS:** a real push through the simulator
- **Android:** a local notification showing the title, text and image

![The Push tool with a payload and the notification on the device](images/push.webp)

## Design tools

Check the screen against the design.

- **Alignment guides:** click a ruler to add one, drag it, and hold Shift to see spacing between guides; choose the color
- **Color picker:** pick any pixel on the device screen; recent colors with copy
- **Inspect:** click any element to see its component chain, dimensions, style and props; **open its source** in your editor; copy each section as JSON
- **Design overlay:** lay a screenshot of the design over the device screen

![The device with alignment guides](images/design-tools.webp)

![The Inspect panel on an element](images/inspect.webp)

## Design overlay

Compare a design with the real screen.

- **Load a design** by choosing it, dropping it, or pasting it (⌘V)
- **Modes:** opacity, swipe with a draggable divider, and difference
- **Fit:** stretch, width or height, then scale and position by hand or with arrow keys
- **Save designs** with a label such as "Login" and reuse them
- **Also on the device:** draw it over the simulator or emulator window itself
- **Esc** stops the overlay

<p align="center"><img src="images/design-overlay-demo.webp" alt="A design laid over the running app, compared by opacity, swipe and difference" width="320"></p>

<p align="center"><sub>Opacity, swipe and difference on the same screen. <a href="images/design-overlay-demo.mp4">Watch it as a video</a>.</sub></p>

![A design laid over the device screen with the divider](images/design-overlay.webp)

## Builds

Install an app on another device without rebuilding.

- **Save** the app from a device as a named build
- **Install** it on another device, optionally removing the app and its data first, and open it afterwards
- **Keep the app's data** with the build and restore it on install
- **Export to a file** and **import** one from another computer
- **Rename and delete** builds

![The Builds tool with two saved builds](images/builds.webp)

## Data snapshots

Save an app's data and put it back.

- **Save** cookies, storage and the rest an app keeps (the cache is never kept)
- **Restore** on the same device or another one, and open the app afterwards
- **Rename and delete** snapshots

![The Data snapshots tool with a snapshot](images/data-snapshots.webp)

## Recording and screenshots

Everything you captured, in one place.

- **Record the screen** or **take a screenshot** from the tool
- **Find saved files:** play, review, copy, show in Finder, delete one or all
- **Mark up screenshots** and **review recordings** (see Quick bar)

![The Recording and screenshots tool with saved files](images/recording.webp)

## Permissions

Grant and revoke permissions on a device.

- **Pick an app** and see the permissions it declares
- **Grant, revoke and reset** each one
- **Refresh** the status

![The Permissions tool for an app](images/permissions.webp)
