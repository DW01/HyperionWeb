---
title: Creating your own plugin
description: Writing a plugin for Hyperion Engine.
lede: Writing a plugin for Hyperion Engine.
summary: Layout, modules, and what a plugin can register.
---

::: note
Plugins are built with the engine for now, so you can develop yours inside of the engine's `Source/Plugins` folder alongside other built-in plugins.
:::

## Layout

Make a folder in `Source/Plugins` named after your plugin:

```text
MyPlugin/
  MyPlugin.hypplugin
  Source/
    MyPlugin/          runtime module
    MyPluginEditor/    editor module (optional)
  Managed/             C# (optional)
  Content/             assets (optional)
  Tests/
```

Every folder under `Source` is a *module*, and the engine's build finds each of them.
Ensure you run the build script (`build.bat` / `build.sh`)  and press `Y` to reconfigure CMake after adding one, as well as when you add or remove a file/folder in here.

:::note
A module whose name ends in `Editor` is only built into the editor. A module built for the editor **may** use the runtime modules, but a runtime module **cannot** use an editor module!
:::

## The descriptor

`MyPlugin.hypplugin` is an HMF file:

```text
PluginDescriptor "MyPlugin" {
    Version = "1.0.0"
    Description = "A plugin that does something."
    EnabledByDefault = false
}
```

| Setting | What it does |
|---|---|
| Version | Shown in the Plugins window. |
| Description | Shown in the Plugins window. |
| EnabledByDefault | Whether new projects have it on. |
| Dependencies | Names of plugins this one needs, they will come along for the ride. |
| EngineMinVersion | The oldest engine version it works with. |

## A module

Each module is a class that implements `IPluginModule`, plus one macro to register it. `OnLoad` runs when the plugin is enabled, and gets a `PluginContext` to register things through:

```cpp
#include <Plugins/PluginModule.hpp>
#include <Plugins/PluginContext.hpp>

namespace Hyperion {

class MyPluginModule final : public IPluginModule
{
public:
    void OnLoad(PluginContext& context) override
    {
        context.RegisterWorldSystem<MySystem>();
    }
};

} // namespace Hyperion

HYP_DEFINE_PLUGIN_MODULE(MyPlugin, MyPlugin, ::Hyperion::MyPluginModule)
```

The `HYP_DEFINE_PLUGIN_MODULE` macro takes the plugin's name, the module's name (the folder name) and the class. Anything you register through the context is removed again when the plugin unloads.

## What a plugin can register

| Call | What it does |
|---|---|
| `RegisterWorldSystem<T>()` | Adds a [system](/docs/world/systems.html) to every world. Optionally limit it to worlds with certain flags, or by a predicate. |
| `RegisterModelImportProcessor<T>()` | Runs after a model is imported, to add components or tweak the result. It can have its own import settings. |
| `AddCleanup(fn)` | Runs when the plugin unloads, for anything you set up yourself. |

Components and other reflected classes (`HYP_CLASS`, `HYP_STRUCT`) register themselves, like they do in a game. Files in `Content` are added to the engine's assets. If you need to know where you're running, `IsEditorHost()` and `GetHostMode()` on the context tell you.

## Editor modules

In an `Editor` module, `RegisterEditorExtension<T>(context)` adds an `EditorExtension`. It gets `Update`, `DebugDraw` and picking hooks for the viewport. There are similar calls for dropping assets onto entities and for setting up a new player.

## Editor UI in C#

Editor panels and menus are written in C# with Avalonia, in the plugin's `Managed` folder. Mark a class with `[EditorPlugin]` and implement `IEditorPlugin`:

```csharp
[EditorPlugin("MyPlugin")]
public sealed class MyPluginEditor : IEditorPlugin
{
    public void Register(EditorPluginRegistry registry)
    {
        registry.RegisterView<MyPanelViewModel, MyPanelView>();
        registry.AddToolMenuItem("My Panel...", new RelayCommand(
            () => PanelService.Instance.OpenPanel(new MyPanelViewModel())));
    }
}
```

The registry also lets you add:

| Call | What it does |
|---|---|
| AddNodeMenuItem | An entry in the Scene panel's right-click menu. |
| AddDocument | A document that docks in the editor, like AnimToolkit's graph editor. |
| AddEditModeBar | A bar that shows in a custom edit mode. |
| RegisterPropertyEditor | A custom Inspector control for fields marked with `EditorType = "..."`. |
| AddComponentInspectorItem | An extra row under a component in the Inspector. |
| AddInspectorWarning | A warning the Inspector shows for an entity. |
| AddCreatableAssetClass, RegisterAssetIcon | Make an asset type creatable from **Add...** and give it an icon. |
| AddEntityDropAssetClass | Let an asset type be dropped onto entities. |

## Examples

AnimToolkit in `Source/Plugins/AnimToolkit` is the full-size one. For something small to copy, `Tests/Plugins/PluginTest` has a system, an import processor, an editor extension, a panel and some content, in about a dozen files.
