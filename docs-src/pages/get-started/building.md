---
title: Build the engine
description: Install the prerequisites and build Hyperion Engine and its editor on Windows, macOS or Linux.
lede: Installing prerequisites and getting the build going
summary: Prerequisites and build commands.
---

## What you'll need

On every platform:

- **CMake** 3.27 or newer.
- **.NET SDK**, with `dotnet` on your PATH. The editor UI is built with Avalonia on .NET 10, so the editor needs it.

Per platform:

| Platform | You'll also need |
|---|---|
| Windows | Visual Studio 2026 (MSVC, or the Clang that ships with it), and [vcpkg](https://github.com/microsoft/vcpkg) with the `VCPKG_ROOT` environment variable pointing at it. |
| macOS | The **Vulkan SDK**, plus `brew install molten-vk` (or run `Tools/Scripts/InstallDependenciesMac.sh`). MoltenVK translates Vulkan to Metal for us. |
| Linux | GCC or Clang, the **Vulkan SDK** with `VULKAN_SDK` set, and the X11, OpenAL and Vulkan loader dev packages. On Ubuntu/Debian: `sudo apt install libx11-dev libopenal-dev libvulkan-dev`. Ninja is optional. |
| Android | The Android NDK (we test with NDK 29), and Ninja on your PATH. See [Android](/docs/platforms/android.html). |
| Web | [emsdk](https://emscripten.org/docs/getting_started/downloads.html) with the `EMSDK` environment variable pointing at it, and Ninja on your PATH. |

## Build it

From the root of the repo:

### Windows

```shell
build.bat Release
```

To build with Clang instead of MSVC: `build.bat Release Clang`

On Windows the default rendering backend is DirectX 12. To build with Vulkan instead, add `Vulkan` (`build.bat Release Vulkan`); that needs the **Vulkan SDK** installed, with `VULKAN_SDK` set.

### macOS

```shell
./build.sh Release
```

To generate an Xcode project: `./build.sh Xcode Release`

### Linux

```shell
./build.sh Release
```

CMake uses your system's default compiler, usually GCC. To use Clang, set `CC=clang CXX=clang++` first. Add `ninja` (`./build.sh Release ninja`) to build with Ninja instead of Makefiles.

::: note
The script asks if you want to regenerate the CMake project first, and moves on without it after 3 seconds. Answer yes if you've added or removed source files. Pass `Regenerate` to always regenerate, or `NoWait` to skip the question.
:::

Use **Release** (or RelWithDebInfo) on Windows. Debug builds work, but run very slowly.

### Other options

| Argument | What it does |
|---|---|
| `Shipping` | An optimized build without the editor, tests or commandlets. See [packaging](/docs/platforms/packaging.html#about-shipping-builds). |
| `Runtime` | The engine without the editor (.NET stays on, for C# games). Goes to `Binaries/<Platform>-Runtime/`. |
| `Android` | Builds for Android. |
| `Web` | Builds for the browser (WebAssembly and WebGPU). |
| `ARM64` | Builds for Windows on ARM. Needs the **C++ Clang tools for Windows** Visual Studio component. |
| `Ninja` | Uses Ninja and clang-cl instead of a Visual Studio solution. |

## CodeGen

CodeGen is a build tool that reads the engine's headers and generates the reflection, serialization and scripting bindings. It runs automatically when CMake configures, so you don't normally run it yourself.

Its output goes into `Source/Generated/`. Don't edit those files by hand; they're overwritten on every run.

## Run it

Build output goes to `Binaries/<Platform>/<Config>/`, for example `Binaries/Windows/Release/`, `Binaries/Mac/Release/` or `Binaries/Linux/Release/`. The main executables are:

- `Hyperion.Editor` (`.exe` on Windows), the editor.
- `hyperion-sample` (`.exe` on Windows), the C++ sample game.
- `CSharpGame` (`.exe` on Windows), the C# sample game.

Commandlets like `PrecompileShaders` land in the same folder. See [Console & CVars](/docs/editor/console.html#commandlets).

## Troubleshooting

- **"VCPKG_ROOT not set"**: Windows builds need it. Point it at your vcpkg install, then open a new terminal.
- **CMake fails with CodeGen errors**: run `Tools/Scripts/BuildCodeGen.bat` (or `.sh`) on its own to see what actually went wrong.
- **Metal API validation errors on macOS**: the generated Xcode project turns Metal API Validation off for you. If you've made your own scheme, turn it off under the Options tab. Rendering goes through MoltenVK, which the validator reports false errors for.

The full [Compiling the Engine]({{engineRepo}}/blob/dev/Documentation/CompilingTheEngine.md) guide in the repo covers Android, optional dependencies and IDE setup.
