---
title: Lights & shadows
description: Light types in Hyperion Engine, their shadow options, and baking static shadow maps.
lede: Directional, point, spot and area lights, and how their shadows are rendered.
summary: Light types and shadow options.
---

## Adding a light

Use :icon[add] **Add › Lighting** in the toolbar:

| Light | What it's for |
|---|---|
| Directional Light | Light from far away, like the sun. Every new project has one. |
| Point Light | Light from a point, in every direction. |
| Spot Light | Light from a point, in a cone. |
| Rectangular Area Light | Light from a rectangle, like a window or a panel. |

## Shadows

Each light has flags in the Inspector:

| Flag | What it does |
|---|---|
| Render shadows | The light casts shadows. On by default. |
| Cache shadow maps for static objects | Static objects' shadows are rendered once and reused, so only moving objects are redrawn each frame. On by default. |
| Only render shadows for static objects | Moving objects don't cast shadows from this light. |
| Bake static shadow map | Bakes static objects' shadows ahead of time. Only for static point and spot lights. |

### Baked static shadows

Enabling **Bake static shadow map** bakes the light's shadow map in the editor.
To rebake every light that has this flag, use :icon[heat] **Bake › Static Shadows**.

