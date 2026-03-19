# cordova-plugin-force-camerax

A Cordova plugin that forces CameraX and LiteRT (TensorFlow Lite) dependencies to specific versions with 16KB page alignment support, required for Android 15+ compatibility.

## Why

Android 15 introduced support for devices with 16KB memory page sizes. Some older library versions ship native `.so` files whose ELF LOAD segments are only 4KB-aligned, causing crashes on 16KB-page devices. This plugin pins the affected libraries to versions that are properly 16KB-aligned.

## What it does

Injects a Gradle resolution strategy that forces these artifacts to 16KB-compatible versions:

**CameraX** (forced to `1.4.2`):
- `androidx.camera:camera-core`
- `androidx.camera:camera-camera2`
- `androidx.camera:camera-lifecycle`

**LiteRT** (forced to `1.4.2`):
- `com.google.ai.edge.litert:litert`
- `com.google.ai.edge.litert:litert-api`

LiteRT is Google's rebranded TensorFlow Lite. Genius Scan SDK 5.8.0 declares a dependency on `litert:1.0.1`, whose `libtensorflowlite_jni.so` has 4KB LOAD segment alignment on `armeabi-v7a`, `x86`, and `x86_64`. Forcing to `1.4.2` brings all four ABIs into compliance.

## Platform support

Android only.
