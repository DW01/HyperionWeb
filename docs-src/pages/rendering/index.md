---
title: Rendering & lighting
description: An overview of rendering in Hyperion Engine: DirectX 12, Vulkan and WebGPU, clustered shading, baked lightmaps, realtime GI and HLSL shaders.
lede: 
summary: Materials, lights, baked lighting, GI, shaders and post-processing.
hero: /assets/editor-scene.jpg
hero_alt: A brick-walled room with a red sphere, coloured boxes and a pillar, in the Hyperion editor viewport
hero_crop: 717 232 1830 773
---

## Overview

- **Glimmer realtime GI**: Hyperion's own global illumination, on by default. Bounce light and sky occlusion are traced in compute shaders, so there's nothing to bake and no ray tracing hardware needed. It runs on desktop and in the browser, and relights instantly when the sun or sky changes. See [Glimmer](/docs/rendering/global-illumination.html#glimmer).
- **Backends**: DirectX 12 is the default on Windows, and Vulkan is used everywhere else (Linux, Android, and through MoltenVK on Apple platforms). Windows builds can also use Vulkan. Web builds use WebGPU.
- **Clustered deferred shading** supports large numbers of dynamic lights. Translucent materials use a forward clustered pass.
- **Baked lighting** comes from the lightmapper built into the editor, along with reflection and irradiance probes for moving objects. Glimmer lights everything that isn't lightmapped.
- **Ray tracing**: HWRT-supported devices can also use DDGI and ray traced reflections. For non-HWRT we have screen space reflections. _Screen space global illumination deprecation is planned so it is not recommended to use_
- **Shaders** are written in HLSL, compiled with DXC, and reload live in the editor on save.

## In this section

::: cards
children
:::
