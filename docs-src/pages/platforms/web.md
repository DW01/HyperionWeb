---
title: Web
description: Build a Hyperion Engine game for the browser with WebAssembly and WebGPU, from the editor or with the BuildWebGame script.
lede: Hyperion games can run in the browser, built to WebAssembly and rendered with WebGPU.
summary: Build your game for the browser.
---

## What you'll need

Web builds are made on Windows (for now), from an editor you [built from source](/docs/get-started/building.html).

- **emsdk**, with `EMSDK` pointing at it. The engine's web build is made with Emscripten 6.0.11.
- **Ninja** on your PATH.
- **PowerShell 7** (`pwsh`), for compressing the cooked content.
- **Python** on your PATH, to serve the build locally.
- The engine built for the web, plus a regular Windows **Release** build (packaging uses its cooking tools):

  ```shell
  build.bat Web Release
  build.bat Release
  ```

The web build checks that the engine's web libraries are newer than its source, and asks you to rebuild them if not.

## From the editor

| Item | What it does |
|---|---|
| :icon[package] **Build › Package for Web** | Cooks your content and builds the game into `Binaries/Web` in your project folder. |
| **Play in Web Browser** (in the :icon[chevron-down] menu next to **Play**) | Builds if needed, then serves the build locally and opens it in your browser. |

The editor can't build C# game projects for the web yet.

`Binaries/Web` is a plain folder of static files, so any static host can serve it as it is. Intermediate files go to `Build/Web`.

New projects limit textures to 256 pixels for the web, to keep downloads small. Change it in [Packaging Settings](/docs/platforms/packaging.html#packaging-settings).

## With the script

`Tools/Scripts/BuildWebGame.ps1` does the same as the editor:

```shell
pwsh Tools/Scripts/BuildWebGame.ps1 -Project Projects/MyGame -Run
```

| Option | What it does |
|---|---|
| `-Run` | Serves the build afterwards and opens it in your browser. |
| `-ServeOnly` | Skips the build, and serves the last one. |
| `-FastLink` | Links at `-O1` instead of `-Oz`: minutes faster, for testing locally. |
| `-MaxTextureSize` | Overrides the texture limit. |
| `-Worlds` | The worlds to include, comma separated. Defaults to the world being edited. |

To serve a build you've already made: `Tools\Scripts\ServeWeb.bat Projects\MyGame` (port 8080 unless you pass another).

## Sample

You can play a web build of our [sample game](/samples.html) right now.
