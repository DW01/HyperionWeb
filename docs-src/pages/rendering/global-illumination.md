---
title: Global illumination
description: Global illumination options in Hyperion Engine: baked lightmaps, Glimmer realtime GI, SSR, GTAO, ray-traced DDGI and reflections, and the console variables that toggle them.
lede: Global illumination is indirect light: light that bounces off surfaces. Hyperion supports several techniques, from fully baked to realtime, with or without ray tracing hardware.
summary: The GI options, and how to toggle them.
---

## Options

| What | What it does | Needs HWRT? |
|---|---|:---:|
| Lightmaps | Baked bounce light for static geometry. See [baking](/docs/rendering/baking.html). | |
| Glimmer | Realtime bounce light and sky occlusion, traced in software. On by default, off on mobile. | |
| SSGI | Bounce light worked out from what's on screen. | |
| SSR | Reflections from what's on screen. | |
| GTAO | Soft shadows in corners and crevices. | |
| DDGI | Realtime bounce light from ray-traced probes. | ✓ |
| RT reflections | Ray-traced reflections, including things that are off screen. | ✓ |

These can be combined. A typical setup is baked lightmaps and probes, with SSR and GTAO on top.

## Glimmer

Glimmer is Hyperion's own realtime GI. It traces rays in compute shaders rather than with ray tracing hardware, and runs on DirectX 12, Vulkan (Windows and macOS) and WebGPU. Nothing needs baking: move the sun or a wall and the bounce light follows.

It's built for static geometry. Moving objects receive its light, but don't affect it.

- Near the camera, probes trace against the scene's meshes. They're placed around solid geometry, so light doesn't leak through walls.
- Further out, a coarser grid traces a voxelized version of the scene, plus a heightfield for terrain.
- Changing the sun or sky relights the scene without tracing it again.
- Static point and spot lights add their bounce light
- Lightmapped surfaces keep their lightmaps. Glimmer lights everything else.
- Sky reflections are dimmed where the sky is blocked, so interiors don't glow with sky color.

It's meant for large outdoor worlds, where baking isn't practical. Turn it off per world with **Glimmer GI** in **World Settings**, or scale it with `Rendering.Glimmer.Intensity`.

On lower-end devices and on the web, the near-field probes are turned off and only the coarser grid is used. See [device tiers](/docs/platforms/#device-tiers).

## Toggles

Each has a console variable. Toggle them from the [console](/docs/editor/console.html); `Config/EngineConfig.json` and the [device tiers](/docs/platforms/#device-tiers) can change their defaults:

| CVar | Controls |
|---|---|
| Rendering.LightmapVolumes | Baked lightmaps |
| Rendering.Glimmer.Enabled | Glimmer |
| Rendering.SSGI | SSGI. Off in the default config. |
| Rendering.SSR | SSR. Off in the default config. |
| Rendering.GTAO | GTAO |
| Rendering.DDGI | DDGI. Off by default. |
| Rendering.RayTracing.RayTracedReflections | RT reflections. Off by default. |

Glimmer, DDGI and ray-traced reflections are also set per world, under **World Settings** in the :icon[settings-gear] gear menu. Glimmer and ray-traced reflections start on there; DDGI starts off.
