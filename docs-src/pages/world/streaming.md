---
title: World streaming
description: How world streaming works in Hyperion Engine: the world grid, streaming cells, and placing scenes on the grid.
lede: Stream content into the world dynamically
summary: Stream content into the world dynamically
---

## How it works

Every world has a **world grid**, made up of one or more **layers**. Each layer is a grid of **streaming cells**.

Cells within range of a **streaming volume** are loaded (and cells out of range are unloaded). Cameras have one, and in multiplayer the server keeps one around each connected player.

## Putting a scene on the grid

Each scene has a **streaming centroid**: the grid cell it belongs to. Set it in the scene's properties in the editor, and when the scene is added to the world, it lands on the built-in scenes layer at that spot.

## Layer settings

Each layer has these settings:

| Setting | What it does |
|---|---|
| cellSize | How big each cell is. Defaults to 32. |
| maxDistance | How far out from the volume's cell to load, counted in cells. Defaults to 1. The terrain layer uses 8. |
| infinite | Whether the grid goes on forever. Useful for infinite terrain generation. Defaults to on. |
| range | The cells the grid covers when it isn't infinite, as a min and max used for both axes. Defaults to -10 to 10. |
