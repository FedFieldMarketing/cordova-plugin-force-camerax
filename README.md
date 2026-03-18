# cordova-plugin-force-camerax

A Cordova plugin that forces CameraX and TensorFlow Lite dependencies to specific versions with 16KB page alignment support, required for Android 15+ compatibility.

## Why

Android 15 introduced support for devices with 16KB memory page sizes. Some older library versions ship native `.so` files whose ELF LOAD segments are only 4KB-aligned, causing crashes on 16KB-page devices. This plugin pins the affected libraries to versions that are properly 16KB-aligned.

## What it does

Injects a Gradle resolution strategy that forces these artifacts to 16KB-compatible versions:

**CameraX** (forced to `1.4.2`):
- `androidx.camera:camera-core`
- `androidx.camera:camera-camera2`
- `androidx.camera:camera-lifecycle`

**TensorFlow Lite** (forced to `2.16.1`):
- `org.tensorflow:tensorflow-lite`
- `org.tensorflow:tensorflow-lite-api`
- `org.tensorflow:tensorflow-lite-support`
- `org.tensorflow:tensorflow-lite-task-vision`
- `org.tensorflow:tensorflow-lite-task-text`

The TensorFlow Lite entries address the `libtensorflowlite_ini.so` (JNI init library) 4KB alignment issue that surfaces when a plugin or SDK (e.g. Genius Scan) pulls in an older TF Lite version as a transitive Maven dependency.

> **Note:** This resolution strategy only works when TF Lite arrives as a transitive Maven dependency. If a third-party SDK bundles `libtensorflowlite_ini.so` directly inside its AAR, only an updated release of that SDK will fix the alignment.

## Platform support

Android only.
