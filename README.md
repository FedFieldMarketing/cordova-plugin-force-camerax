# cordova-plugin-force-camerax

A Cordova plugin that forces CameraX dependencies to a specific version with 16KB page alignment support, required for Android 15+ compatibility.

## Why

Android 15 introduced support for devices with 16KB memory page sizes. Some older CameraX versions are not aligned to 16KB pages and will crash on these devices. This plugin pins CameraX to a compatible version across all transitive dependencies in your Cordova app.

## What it does

Injects a Gradle resolution strategy that forces these CameraX artifacts to version `1.4.2`:

- `androidx.camera:camera-core`
- `androidx.camera:camera-camera2`
- `androidx.camera:camera-lifecycle`

## Platform support

Android only.
