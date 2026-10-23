---
title: Platforms
description: Platforms supported by Hyperion Engine
lede: But will it Hyperion?
summary: Supported platforms, packaging and platform notes.
---

## Where it runs

| Platform | Status |
|---|---|
| Windows (x64, ARM64) | Yes. Runtime and editor. DirectX 12 by default, or Vulkan. |
| macOS | Yes. Runtime and editor. |
| Web | Yes, through WebAssembly and WebGPU. Runtime only, built from the Windows editor. |
| Android | Supported - not stable yet. |
| iOS | Supported - not stable yet. |
| Steam Deck | Yes, through Proton. Input and resolution handling still need work. |
| Linux | *Planned* |

The engine compiles on Linux with GCC, but it isn't a supported platform yet. [Contributions](/docs/contributing/) are welcome on this front (as well as anywhere else)

## In this section

::: cards
children
:::


## Steam Deck

There's no native Linux build yet, so on the Deck you run the Windows build through Proton. Controller input and resolution handling still need work here

## Per-platform settings

Each platform can have its own config, like `Config/EngineConfig.Android.json` or `Config/GlobalConfig.Web.json`. If a platform file exists it *replaces* the regular one, rather than merging with it, so it needs every setting.

The mobile configs, for example, turn off ray tracing, DDGI, SSGI and TAA.

## Device tiers

On top of the config, `Config/DeviceTiers.hmf` has rules that change settings for the device the game is running on. Each rule matches on any of:

| Axis | Values |
|---|---|
| DeviceType | Desktop, Laptop, Mobile |
| DevicePlatform | Windows, MacOS, Linux, Android, IOS, Web |
| DeviceGrade | Low, Medium, High, Ultra |

and overrides the `EngineConfig` settings it lists. `When` matches exact values, and `AtMost` matches a grade or anything below it:

```
TierRule "Web" {
    When = { DevicePlatform = Web }
    Set = {
        "Rendering.Glimmer.Probes.Enabled" = false
    }
}
```

The Mobile rule, for example, turns off Glimmer, SSR, clouds, fog volumes, shadows and bloom.

To test another tier, force an axis from the command line with `--devicetype`, `--deviceplatform` or `--devicegrade`, like `--devicegrade=Low`.
