---
title: Prefabs
description: Create prefabs from nodes in the Hyperion editor, place them in your scenes, and update them.
lede: A prefab is a reusable group of nodes that you can place in any scene.
summary: Creating, placing and updating prefabs.
---

## Making a prefab

::: steps
1. In the **Scene** panel, right-click a node and pick **Save as Prefab...** Select a few nodes first to bundle them together.

2. Give it a name (no spaces) and hit **Create**.
:::

The node you started with becomes an instance of your new prefab. It's marked with :icon[prefab] in the Scene panel.

To create an empty prefab: **Assets › Add... › Prefab**.

## Placing it

Drag the prefab from **Assets** into the viewport, or right-click it and pick **Add to Current Scene**.

## Making changes

Tweak an instance, then right-click it and choose **Sync Prefab** to update the prefab itself.

To add nodes to an existing prefab, select them, right-click, and pick the prefab under **Add to Prefab**.

To edit a prefab on its own, right-click an instance and choose **Edit Prefab**. The prefab opens in place of your scene; when you're done, pick **Exit Prefab Edit** from the dropdown at the top of the Scene panel.

All of these actions can be undone.
