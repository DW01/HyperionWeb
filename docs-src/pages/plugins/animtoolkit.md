---
title: AnimToolkit
description: The AnimToolkit plugin for Hyperion Engine: skeletal animation, animation graphs, character models, retargeting and the animation editor.
lede: Everything for animated characters: playing clips, blending them with graphs, and editing them in the editor.
summary: Skeletal animation, graphs and the animation editor.
---

::: note
This doc is a work in progress.
:::

AnimToolkit includes two modules. **Animation**, which your game uses at runtime, and **AnimationEditor**, which only the editor loads, for in-editor tooling.

::: note
Without the plugin, skinned meshes still import and draw in their bind pose, and clips still import as assets. They just don't play.
:::

## Playing a clip

Add an `AnimationComponent` to an entity with a skinned mesh. Pick a clip under `Animation`, and tick `PlayOnStart` to have it play when the game starts.

| Setting | What it does |
|---|---|
| Animation | The clip to play. The list only shows clips that fit the entity's skeleton. |
| PlayOnStart | Start playing when the game starts. |
| LoopMode | Whether the clip plays once or loops. |
| Speed | Playback speed. 1 is normal. |
| Graph | An animation graph to run instead of a single clip. See below. |

Importing a model with animations adds the `AnimationComponent` for you, set to the first clip. You can turn that off in the import settings with `AddAnimationComponent`.

If a clip was made for a different skeleton, or there's no skeleton at all, the Inspector shows a warning.

## Animation graphs

An animation graph decides which pose a character shows. Instead of switching clips by hand, you build a graph once, then drive it with a few **parameters** like `Speed` or `Jump` from your game.

Create one from **Assets › Add... › Animation Graph**. Double-click a graph in **Assets** to open it.

### Nodes

A graph is a set of nodes that each produce a pose. Wire them together and mark one as the **output**.

| Node | What it does |
|---|---|
| Clip | Plays a clip, with a play rate, looping and a start offset. |
| Blend1D | Blends clips placed along one parameter, like idle, walk and run on speed. |
| Blend2D | Blends clips over two parameters, like forward and sideways velocity. |
| Layer | Plays one pose over another, only on the bones in a **bone mask**. |
| Additive | Adds a pose on top of a base pose. |
| ChainTwist | Twists a chain of bones, for aiming. |
| Slot | A place for gameplay to play a one-off clip, like an emote, over the graph. |
| FootIK | Plants the feet on the ground. |
| StateMachine | Moves between states, each with its own pose. |

Clips in a **sync group** share their phase, so blended walk and run cycles keep their feet in step.

### State machines

Double-click a StateMachine node to open it. States are boxes and transitions are arrows. Right-click a state and pick **Make Transition**, then click the state it leads to.

Each transition has a duration, a blend curve, a priority, and conditions that read like sentences: `Speed > 0.5`, `Jump is triggered`, `time in state >= 0.3s`.

### Parameters

The Parameters panel lists the values your game sets. They can be floats, bools, triggers or vectors. While you're editing, drag a value and watch the preview character blend.

## Character models

`CharacterModelComponent` drives a character from its character controller. It works out speed, direction, whether it's in the air and so on, and feeds them to the graph. It also handles which way the character faces, turn-in-place steps and aiming.

By default it runs the built-in `HumanoidMotionMatching` graph, so a humanoid character animates with no setup. To use your own, set `Graph`.

| Setting | What it does |
|---|---|
| Graph | The animation graph to run. |
| FacingMode, TurnSharpness | Which way the body faces, and how quickly it turns to it. |
| AlignToCapsule, ModelOffset | Where the model sits inside the character controller's capsule. |
| FootIK | Plants the feet on uneven ground. `FootProbeHeight`, `FootProbeDepth` and `FootIKSmoothing` tune it. |
| ApplyRootMotion | Moves the character with the motion baked into the clip. |

## Humanoids and retargeting

A skeleton can be marked as a **humanoid** by mapping its bones to standard slots like hips, spine and the arm and leg chains. The editor can map common rigs for you.

Once two skeletons are mapped, a clip made for one plays on the other. Rotations carry over bone by bone, and the hips movement is scaled to fit the new character's height.

## Bone attachments

Put a `BoneAttachmentComponent` on an entity to make it follow a bone or **socket** of another character, like a sword in a hand. Sockets are named points on a skeleton, with an offset from their bone.

## Using it from the editor

### Editing animation

Right-click an animated entity and pick **Edit Animation**, or double-click a skeleton or clip in **Assets**. The editor opens a preview of the character:

- the hierarchy shows its bones, and you can add sockets to them;
- a timeline bar under the viewport plays the clip and lets you scrub and add markers;
- **Show Bones** in the tools menu draws the skeleton in the viewport.

Make your changes, then **Apply** to save them or **Revert** to throw them away.

### Editing a graph

Right-click an entity and pick **Edit Animation Graph**, or double-click a graph in **Assets**. The graph opens in the bottom dock beside **Assets** and **Console**, with the viewport and preview character above it.

- Press <kbd>Space</kbd> on the canvas to search for a node to add.
- Select a node to edit its settings in the main **Inspector**.
- Press <kbd>Home</kbd> to frame the whole graph.

Graphs that come with the engine are read-only. Use **Copy to Project** to get an editable copy that's assigned to your character.

### Debugging while playing

On a `CharacterModelComponent` or `AnimationComponent`, **Open Graph** attaches the graph to the running character. The current state, running transitions and node weights light up as you play, and the Parameters panel shows live values.

::: soon
- Picking which character to debug
- Opening a new graph as soon as it's created
:::
