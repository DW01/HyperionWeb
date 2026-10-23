---
title: A tour of the codebase
description: A quick tour of the Hyperion Engine repository
lede: What goes where?
summary: What lives where in the repo.
---

## Top-level directories

| Folder | What's in it |
|---|---|
| Source | All the engine and editor code |
| Config | Engine and runtime settings (`EngineConfig.json`, `GlobalConfig.json`) and their per-platform versions, device tier rules (`DeviceTiers.hmf`), and the list of shaders to compile (`Shaders.hmf`). |
| Content | Assets for the core engine and editor |
| External | Third-party code: Git submodules and prebuilt libraries. |
| Tools | Build and packaging scripts, CodeGenTool source and other misc tools |
| Documentation | Longer guides, like compiling the engine and the console, and third-party licenses. |
| Build, Binaries | Where your build output goes **Not committed, these are excluded via .gitignore** |
| PackagedBuilds | Output of the [packaging scripts](/docs/platforms/packaging.html#with-the-packaging-scripts). Also not committed. |

## `Source` structure

| Folder | What's in it |
|---|---|
| Core | containers, memory, reflection and so on. Keeps its dependencies to a minimum. This is also re-used in our CodeGenTool, not tied to the engine |
| Engine | The main engine library: rendering, scenes, physics, networking, scripting and so on. |
| Editor | The editor's code. C++ and C# mixed (bindings are C++, actual editor UI is C#) |
| Shaders | HLSL shaders, compiled with DXC. |
| Commandlets | See [console](/docs/editor/console.html#commandlets) |
| Sample | The sample games: `DefaultGame` (C++, builds `hyperion-sample`) and `CSharpGame` (C#) |
| Templates | The templates the editor uses to [generate game projects](/docs/editor/build-game.html), in C++ and C#, and the web page for web builds |
| PlatformSpecific | Per-platform projects, like the Android Gradle project |
| Generated | CodeGen output. Don't edit by hand, it'll be overwritten on  next cmake configure! |
