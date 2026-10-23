---
title: Android
description: Build Hyperion Engine for Android: requirements, building the native libraries, packaging content and making an APK with Gradle.
lede: Hyperion runs on Android phones and tablets. Support works, but isn't stable yet.
summary: Building and installing on Android devices.
---

## What you'll need

- The **Android NDK**. We test with NDK 29. Point `ANDROID_NDK_HOME` at it.
- **Ninja**, on your PATH or installed with Visual Studio or the Android SDK.
- The **Android SDK** and **Java 17**, for Gradle. Android Studio installs both.
- A regular Windows **Release** build of the engine (`build.bat Release`). Packaging uses its shader and cooking tools.

We build for 64-bit ARM (`arm64-v8a`), and you'll need Android 9 (API 28) or newer.

## Build it

::: steps
1. Build the engine for Android and package it with your project's content:

   ```shell
   Tools\Scripts\PackageBuildAndroid.bat --cook --project MyGame
   ```

   This makes its own shipping build for Android, so you don't need to run `build.bat Android` first. `--project` is the project's folder name under `Projects/`. Without `--cook`, only engine content is included. `--skip-precompile` skips precompiling shaders.

   The package lands in `PackagedBuilds/Android/Build_<date>_<time>/`.

2. Build and install the APK with Gradle, from `Source/PlatformSpecific/Android/`:

   ```shell
   gradlew.bat installDebug
   ```

   Gradle picks up the last package automatically. You can also open that folder in Android Studio and run it from there.
:::

To build only the engine libraries, without packaging: `build.bat Android Release`. They end up in `Binaries/Android/Release/`.

## Settings

Android uses `Config/EngineConfig.Android.json` instead of the regular config with platform-specific overrides for targeting lower end devices than the typical desktop experience. 

The Mobile [device tier](/docs/platforms/#device-tiers) rule applies on top of it.
