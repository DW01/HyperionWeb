---
title: Scripting
description: Writing gameplay scripts for Hyperion Engine in Strata or C#, and exposing C++ types to them.
lede: Gameplay scripts can be written in Strata or C#
summary: Gameplay scripts in Strata or C#, and exposing C++ to them.
---

Hyperion supports scripting with C#. Scripts can be attached to individual objects to define behaviour.

## Exposing C++ to scripts

Engine types show up in both languages through reflection. Add a class in C++ with reflection macros, and Hyperion's CodeGenTool generates binding code so you can use it in scripts.

```cpp
HYP_CLASS()
class Camera : public Entity
{
    HYP_OBJECT_BODY(Camera);
public:
    HYP_METHOD(Property = "FOV")
    float GetFOV() const;

    HYP_METHOD(Property = "FOV")
    void SetFOV(float v);
};
```


## In shipped games

When you [package](/docs/platforms/packaging.html) a game, C# scripts are compiled ahead of time with NativeAOT, so the game doesn't need .NET installed.

## In this section

::: cards
children
:::
