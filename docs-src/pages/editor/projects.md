---
title: Working with projects
description: Create, open and save projects in the Hyperion editor, organize assets in folders, and see what goes inside a project folder.
lede: A project holds your game's scenes, assets, scripts and settings in one folder.
summary: Making, opening and saving projects, and what's inside.
---

## The start screen

The editor opens on a start screen:

- **New Project** makes a project from the blank template.
- **Browse...** opens an existing `.hypproject` file.
- **Recent Projects** lists what you've opened before. Use the arrow keys and <kbd>Enter</kbd> to pick one. Right-click one to pin it, show it in Explorer, or remove it from the list.

Tick **Open last project on startup** to skip the start screen next time. To turn that back off, untick **Always Open Most Recent Project on Startup** under the arrow next to :icon[folder-opened] **Open** in the toolbar.

## New projects

**New Project** (on the start screen, or :icon[file] in the toolbar) asks where to save the project first, and creates a folder for it named after the project. It starts with a main scene, a sun, the ground, and a player with a camera.

## Opening a project

Use :icon[folder-opened] **Open** in the toolbar and pick a `.hypproject` file, or pick one from the recent projects under its arrow.

## What's inside

```
Projects/MyGame/
  MyGame.hypproject
  AssetFolders.txt
  Content/
    Materials/
    Meshes/
    Prefabs/
    Scenes/
    Scripts/
    Textures/
    Worlds/
  Saved/
```

The `.hypproject` file is the project itself, and `Content` holds your assets, sorted into folders by type. Assets are saved as `.hmf` files, a readable text format, with larger binary data in `.blob` files next to them. `Saved` holds editor state, like the thumbnail on the start screen.

A project with C++ or C# code also has `Source`, `Build` and `Binaries` folders, and packaging adds `Packaged`. See [Building your game](/docs/editor/build-game.html).

::: note
Projects made before the `Content` folder keep their assets next to the `.hypproject` file, and still work as they are.
:::

## The Assets panel

The Assets panel has its own folders, separate from how files are laid out on disk. Make as many as you like and organize assets however you want:

- **Add... › Folder**, or right-click a folder, to make one. Right-click to rename or delete it.
- Drag assets and folders onto a folder, or onto the path at the top, to move them. Moves can be undone.
- **Import...** and **Add...** put new assets in the folder you're in.
- The search box searches the current folder, or everything from the top. Filter by type, and sort by name, date modified or type.

| Key | Action |
|---|---|
| <kbd>Enter</kbd> | Open |
| <kbd>Backspace</kbd> | Up a folder |
| <kbd>F2</kbd> | Rename a folder |
| <kbd>Delete</kbd> | Delete |

These folders are saved in `AssetFolders.txt`, and only the editor uses them.

## Saving

There's no separate "save scene". Saving the project saves everything that's changed, scenes included. The editor camera position is saved with the project too.

Close with unsaved changes, and the editor will ask whether to save, discard, or cancel.
