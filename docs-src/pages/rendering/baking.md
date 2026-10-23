---
title: Baking lighting
description: Bake lightmaps, reflection probes and irradiance probes in the Hyperion editor, and tune the baker settings.
lede: Baking computes lighting ahead of time, so it doesn't have to be calculated while the game runs. It's the main way to get good lighting on lower-end hardware.
summary: Baking lightmaps and probes in the editor.
---

## How to bake

::: steps
1. Add a **Lightmap Volume** around the area you want baked: :icon[add] **Add › Lighting › Lightmap Volume**.

2. For lighting and reflections on moving objects, add **Reflection Probes** and **Irradiance Probes** from the same menu.

3. Click :icon[heat] **Bake** in the toolbar and pick what to bake: **Lightmaps**, **Reflection Probes**, **Irradiance Probes**, **Fog Volumes** or **Static Shadows**.
:::

Progress is shown in an overlay while the bake runs.

When you change something a bake depends on, like moving a static object or a light, the editor shows what needs a rebake in an overlay.

## What gets baked

| Type | What it is |
|---|---|
| Lightmaps | Light bouncing around your static geometry, saved into textures. Lightmap UVs are generated for you. |
| Reflection probes | What the world looks like from a point, for shiny surfaces. |
| Irradiance probes | How much light reaches a point, for lighting things that move. |
| Fog volumes | Light from static lights scattering through fog volumes. |
| Static shadows | Shadow maps for static point and spot lights with **Bake static shadow map** ticked. See [lights & shadows](/docs/rendering/lights.html#baked-static-shadows). |

Baking runs on the GPU. It uses hardware ray tracing when available, and compute shaders otherwise.

## Settings

Bake settings live in the `"Baker"` section of `Config/EngineConfig.json`:

| Setting | What it does |
|---|---|
| NumSamples | More samples, less noise, longer bakes. The default config uses 1. |
| MaxRayDistance | How far rays travel looking for light. Defaults to 1000. |
| ForceComputeTracing | Use the compute path even when hardware ray tracing is available. Also the `Baking.ForceComputeTracing` CVar. |

::: note
Each [swatch](/docs/world/swatches.html) has its own bake.
:::
