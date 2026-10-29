---
title: Building your game
variant: C++
description: Generate a C++ game project from the Hyperion editor, build it, and run your game as its own executable, in single player or multiplayer.
lede: Give your project its own C++ code, and build it into a game you can run outside the editor.
summary: Generate a C++ or C# project, build it, and run your game outside the editor.
---

## The Build menu

:icon[package] **Build**, near the right end of the toolbar, has everything on this page.

![The Build menu, open in the editor toolbar](/assets/docs-build-menu.png)

| Item | What it does |
|---|---|
| Generate Game Project... | Adds a C# or C++ project to your project folder. Once it exists, this becomes **Open C# Project Folder** or **Open C++ Project Folder**. |
| Change Language... | Switches the project between C# and C++. Only applicable when source files haven't been changed. |
| Build Game | Compiles that project into a game executable. |
| Reload Game | Loads the latest build of your C++ game into the editor. See [In the editor](#in-the-editor). |
| Package Game | Makes a standalone copy of the game to share. See [Packaging a build](/docs/platforms/packaging.html). |
| Package for Web | Builds the game for the browser. See [Web](/docs/platforms/web.html). |
| Packaging Settings... | Settings for packaged builds - see [Packaging settings](/docs/platforms/packaging.html#packaging-settings). |

This page covers C++; switch to C# at the top of the page.

::: note
This page uses Windows paths. On Linux and macOS, the build needs CMake and the same C++ compiler the engine was built with (`g++` or `clang++`) on your PATH, and uses Ninja if it's installed. Output goes to `Binaries/Linux/` or `Binaries/Mac/`, executables have no `.exe`, and the build script is `build.sh`.
:::

## Generate the C++ project

Save your project first, then choose **Build › Generate Game Project...** and pick **C++**. The editor adds a `Source` folder to your project and opens it (or opens it in Visual Studio, if **Open in Visual Studio** is ticked):

```
Projects/MyGame/
  MyGame.hypproject
  Source/
    CMakeLists.txt
    Game/
      MyGameGame.hpp
      MyGameGame.cpp
    Launcher/
      main.cpp
```

The names come from your `.hypproject` file's name. These files are yours to edit, and the editor won't overwrite them.

| File | What's in it |
|---|---|
| Game/MyGameGame.hpp, .cpp | Your `Game` class. This is where your game's code goes. |
| Launcher/main.cpp | The executable's entry point. It starts the engine and creates your `Game`. |
| CMakeLists.txt | Builds the two above against the engine. Every `.cpp` and `.hpp` under `Game/` is picked up automatically. |

## Your Game class

The generated class overrides a few hooks from `Game`:

```cpp
void MyGameGame::OnLaunch()
{
    Game::OnLaunch();

    HYP_LOG(Game, Info, "MyGameGame launched");
}

void MyGameGame::OnUpdate(float delta)
{
    Game::OnUpdate(delta);
}
```

| Function | When it's called |
|---|---|
| OnLaunch | Once, after the startup world has loaded. |
| OnUpdate | Every frame, with the time since the last frame. |
| OnInputEvent | For each input event. Returns `true` if something handled it. |
| BeforeConnectingToServer | When the game starts as a client, before it has joined a server. |
| BeforeContentLoaded, AfterContentLoaded | Either side of loading the startup world. |

The last three drive a plain status screen (`ShowStatus` and `HideStatus` in the same file), so the window says "Loading...", "Connecting to..." or why it couldn't connect instead of sitting black. Swap it for your own loading and connect screens.

::: note
CodeGenTool doesn't run on game code yet, so `HYP_CLASS()` and friends aren't available here. The generated `.cpp` registers the class by hand; leave that block at the bottom of the file in place.
:::

## Build

Choose **Build › Build Game**. Compiler output goes to the [Console](/docs/editor/console.html), and you'll get a message box if the build fails.

The build needs Visual Studio, or the Visual Studio Build Tools, with:

- The **Desktop development with C++** workload.
- **C++ Clang tools for Windows**. Not needed if you built the editor yourself with MSVC.
- **C++ CMake tools for Windows**.

If something's missing, the editor tells you what and offers to install the Build Tools for you.

The result lands in your project's `Binaries` folder:

```
Projects/MyGame/
  Binaries/Windows/
    MyGame.exe
    MyGameGame.dll
    hyperion.dll
    Config/
  Build/Windows/
    Build.bat
```

`MyGameGame.dll` holds your game's code, and `MyGame.exe` is the launcher that loads it. The engine's own libraries and config are copied in next to them. `Build.bat` runs the same build outside the editor.

## Run it

Run `MyGame.exe`. It loads your project's content straight from the project folder, so there's nothing to cook: save in the editor, and the next run has your changes.

By default the game starts in single player. The same executable also hosts and joins multiplayer games:

| Command | What it does |
|---|---|
| `MyGame` | Single player |
| `MyGame --server` | A headless dedicated server |
| `MyGame --singleplayer=false --host=127.0.0.1` | Joins the server at that address |

The single player default comes from `Binaries/Windows/Config/GlobalConfig.json`; anything you pass on the command line overrides it. More in [Running a server](/docs/multiplayer/server.html).

## In the editor

Once the game is built, the editor loads `MyGameGame.dll` when it opens your project, and [play-in-editor](/docs/editor/play-in-editor.html) runs your `Game` class.

### Hot reload

You can rebuild while the project is open. When `MyGameGame.dll` changes, the editor loads the new build by itself, whether you built from the editor, Visual Studio or `Build.bat`.

To force a reload, use **Build › Reload Game**. Either way, it waits until you stop playing, and Play always runs the newest build.

::: note
To turn the automatic reload off, set the `Editor.AutoReloadGameModule` CVar to `false`.
:::

