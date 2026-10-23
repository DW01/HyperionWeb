---
title: A tour of the editor
description: A quick tour of the Hyperion editor: the Scene, Inspector, Viewport, Assets and Console panels, the toolbar, viewport controls and shortcuts.
lede: The editor's panels, toolbar, viewport controls and shortcuts.
summary: The panels, the toolbar, and getting around the viewport.
---

## The panels

| Panel | What it's for |
|---|---|
| Scene | Everything in your scene, as a tree. The dropdown at the top switches between scenes, or adds a new one. |
| Inspector | All about whatever you've got selected: its components, tags, layers, script and properties. |
| Viewport | The 3D view, in the middle of the window. |
| Assets | Your project's content, in folders. Search it, **Import...** things, or make something with **Add...**. See [projects](/docs/editor/projects.html#the-assets-panel). |
| Console | Logs, plus a spot to type commands. See [Console & CVars](/docs/editor/console.html). |

Asset editors open as panels on the right. To restore the default layout, use **Layout › Reset Layout** in the :icon[settings-gear] gear menu.

## The toolbar

There's no menu bar. Everything lives in the toolbar, roughly left to right:

- :icon[file] **New Project**, :icon[folder-opened] **Open** (its :icon[chevron-down] arrow lists recent projects) and :icon[save] **Save**.
- :icon[discard] Undo, :icon[redo] redo, :icon[copy] copy and :icon[clippy] paste.
- :icon[select] **Select All**, with **Select All in Viewport** and **Select None** under its arrow.
- :icon[layers] **Layers**, and :icon[roller] the active [swatch](/docs/world/swatches.html).
- :icon[heat] **Bake**, for [baking lighting](/docs/rendering/baking.html).
- :icon[add] **Add**, for putting new things in your scene: lights, probes, volumes and more.
- :icon[move] **Translate**, :icon[refresh] **Rotate** and :icon[screen-full] **Scale**, to pick what the gizmo does, plus :icon[magnet] grid snapping. The arrow next to snapping has the grid settings: snap size, rotation snap and offset.
- :icon[mesh-edit-mode] Mesh tools, :icon[landscape-edit] terrain tools (sculpting and painting) and :icon[paintbrush] paint tools (decals, instances and ground cover).
- :icon[package] **Build**, for [building](/docs/editor/build-game.html) and [packaging](/docs/platforms/packaging.html) your game.
- :icon[play] **Play**, :icon[debug-pause] **Pause** and :icon[debug-stop] **Stop**. More in [play-in-editor](/docs/editor/play-in-editor.html).
- The :icon[settings-gear] gear menu, with **World Settings**, LOD, **Ghost Mode**, **Show Stats** and **Layout**.

## Viewports

The gear menu's **Layout** picks how many viewports you get:

| Layout | Views |
|---|---|
| Single Viewport | One perspective view. This is the default. |
| Four Viewports | Top and Front above, Side and Perspective below. |
| Perspective + Three | A large perspective view, over a row of Top, Front and Side. |

In the Top, Front and Side views, drag with any mouse button to pan, and scroll to zoom.

## Viewport controls

| Action | Input |
|---|---|
| Look around | Left-drag |
| Pan along the ground | Right-drag |
| Pan up, down and sideways | Left + right drag, or <kbd>Alt</kbd> + drag |
| Fly | <kbd>W</kbd> <kbd>A</kbd> <kbd>S</kbd> <kbd>D</kbd> |
| Let go of the mouse | <kbd>Esc</kbd> |

On a trackpad, hold <kbd>Ctrl</kbd> in place of the right mouse button. Camera speed and mouse sensitivity are set with the `Editor.Camera.MovementSpeed` and `Editor.Camera.MouseSensitivity` CVars.

## Shortcuts

On macOS, use <kbd>Cmd</kbd> in place of <kbd>Ctrl</kbd>.

| Action | Shortcut |
|---|---|
| New project | <kbd>Ctrl</kbd> + <kbd>N</kbd> |
| Open project | <kbd>Ctrl</kbd> + <kbd>O</kbd> |
| Save project | <kbd>Ctrl</kbd> + <kbd>S</kbd> |
| Save project as | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>S</kbd> |
| Undo | <kbd>Ctrl</kbd> + <kbd>Z</kbd> |
| Redo | <kbd>Ctrl</kbd> + <kbd>Y</kbd>, or <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Z</kbd> |
| Copy, paste | <kbd>Ctrl</kbd> + <kbd>C</kbd>, <kbd>Ctrl</kbd> + <kbd>V</kbd> |
| Select all | <kbd>Ctrl</kbd> + <kbd>A</kbd> |
| Select none | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>A</kbd> |
| Delete | <kbd>Delete</kbd> |
