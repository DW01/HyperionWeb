---
title: iOS
description: Build Hyperion Engine for iOS with Xcode and MoltenVK.
lede: Hyperion runs on iPhone and iPad through MoltenVK. Like Android, support isn't stable yet.
summary: Build for iPhone and iPad through Xcode.
---

## What you'll need

- A Mac with **Xcode**.
- The **Vulkan SDK**, with `VULKAN_SDK` set. It comes with MoltenVK, which we link for iOS.
- A device on iOS 14 or newer.

## Build it

From the root of the repo, generate an Xcode project:

```shell
./Tools/Scripts/BuildHyperion.sh IOS Xcode Release regenerate
```

Open it in Xcode, pick your team under **Signing** (we leave signing off by default), and run it on your device.

## Packaging

`Tools/Scripts/PackageBuildIOS.sh` makes a shipping build for iOS and packages it with your project's content. It needs a Mac **Release** build first, for the shader and cooking tools, and asks for your project's folder name under `Projects/`. The package lands in `PackagedBuilds/IOS/Build_<date>_<time>/`.

The script is still a work in progress.

## Notes

- There's no editor on iOS.
- iOS uses `Config/EngineConfig.IOS.json`, which turns off the same rendering features as Android, plus SSR, and targets 30 FPS. The Mobile [device tier](/docs/platforms/#device-tiers) rule applies on top of it.
