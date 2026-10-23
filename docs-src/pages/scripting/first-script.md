---
title: Your first script
description: Create your first script in the Hyperion editor, in Strata or C#, attach it to an entity, and learn the script lifecycle and live reload.
lede: Create a script, attach it to an entity, and make the entity move.
summary: Attach a script to an entity and make it move.
---

## Create a script

::: steps
1. Select an entity in the **Scene** panel.

2. In the **Inspector**, find the **Script** section, open its **More actions** menu, and pick :icon[add] **Create New Script**.

3. Choose the language of the script, and give it a name.
:::

::: note
Strata is temporarily disabled in current builds, so only C# is offered for now.
:::

The editor adds a `ScriptComponent` to the entity, and saves the file to `Content/Scripts/<Name>.strata` or `Content/Scripts/<Name>.cs` in your project. The new script looks like this:

::: tabs
```csharp
using Hyperion;

public class NewScript : Script
{
    public override void OnAdded(Entity entity)
    {
    }

    public override void Update(float deltaTime)
    {
    }

    public override void Destroy()
    {
    }
}
```

```strata
import Engine;

Entity g_entity;

void OnAdded(const Entity entity)
{
    g_entity = entity;
}

void Update(float delta)
{
}

void Destroy()
{
}
```

:::

In C#, the class is named after the script.

## Lifecycle

Both languages use the same three functions. In Strata they're plain functions in the file; in C# they're overrides on `Script`.

| Function | When it's called |
|---|---|
| OnAdded | When play starts. Receives the entity the script is attached to. |
| Update | Every frame while the game is running, with the time since the last frame. |
| Destroy | When the entity goes away, or you stop playing. |

All three are optional.

Each entity gets its own copy of the script's state: its own Strata globals, or its own instance of the C# class. Entities sharing a script don't share state.

## Moving the entity

This moves the entity upward while the game runs:

::: tabs

```csharp
using Hyperion;

public class NewScript : Script
{
    public override void OnAdded(Entity entity)
    {
        base.OnAdded(entity);
    }

    public override void Update(float deltaTime)
    {
        Entity.Translate(new Vec3f(0.0f, deltaTime, 0.0f));
    }
}
```

```strata
import Engine;

Entity g_entity;

void OnAdded(const Entity entity)
{
    g_entity = entity;
}

void Update(float delta)
{
    g_entity.Translate(float3(0.0, delta, 0.0));
}
```
:::

In C#, calling `base.OnAdded(entity)` sets the script's `Entity` property. The editor's template leaves it out, so add it when you want to use `Entity`.

## Live reload

Saving the file recompiles it in the editor, in either language. While playing, entities using the script get `Destroy`, the new code is loaded, and `OnAdded` runs again.

Script state is reset on reload.

If a script throws, it's marked as errored and stops getting `Update` calls, until the script runs without throwing.