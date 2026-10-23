---
title: Samples
description: Sample scripts for Hyperion Engine in Strata and C#.
lede: 
summary: Example scripts
---

To try one of these - create a script in the sample's language (**Inspector › Script ›** **Create New Script**), paste the sample in, and save it

## Health component

A custom component that drains over time. C# only (for now).

::: tabs
```csharp
using Hyperion;

public struct Health : IComponent
{
    public float Current;
    public float Max;
}

public class NewScript : Script
{
    public override void OnAdded(Entity entity)
    {
        base.OnAdded(entity);

        Health health = new Health { Current = 100, Max = 100 };
        entity.AddComponent<Health>(ref health);
    }

    public override void Update(float deltaTime)
    {
        ref Health health = ref Entity.GetComponent<Health>();
        health.Current -= deltaTime;

        Logger.Log(LogLevel.Info, $"Entity health: {health.Current}");
    }
}
```
:::

| Call | What it does |
|---|---|
| `IComponent` | Marks the struct as a component type. It's registered when the script loads. |
| `AddComponent(ref health)` | Adds it to the entity |
| `GetComponent<Health>()` | Returns a `ref`, so changes apply directly |

Component structs must be blittable: plain value fields, no classes, strings or arrays.

By default, a component is saved with the scene and shown in the editor. To change that, add `[Component(Flags = ...)]` to the struct, with any of `ComponentFlags.Serialize`, `ComponentFlags.ShowInEditor` and `ComponentFlags.Replicated`.
