---
title: Replication & prediction
description: How replication works in Hyperion Engine: replicating entities, interpolation and dead reckoning, and client-side prediction for player movement.
lede: The server runs the authoritative game state and sends updates to clients, which interpolate and predict between them.
summary: How the server keeps clients in sync.
---

## Replicating an entity

Add the `Replicated` tag on the server:

```cpp
entity->AddTag<EntityTag::Replicated>();
```

The server assigns it a network ID and sends its transform (plus velocities, for physics bodies) to clients.

Clients only receive updates for entities within 50 units of them.

## Interpolation

Updates don't arrive every frame, so clients render slightly behind and interpolate between the last couple of updates. When updates are late, dead reckoning guesses where things are headed.

| CVar | What it does |
|---|---|
| Net.InterpolationEnabled | Turns interpolation on or off. |
| Net.InterpolationDelay | How far behind to stay, in seconds. Starts at 0.1. |
| Net.DeadReckoning | Turns dead reckoning on or off. |
| Net.InterpRatio | Stays at least this many update intervals behind, if that's more than `Net.InterpolationDelay`. Starts at 2. |

## Client-side prediction

The local player's movement is predicted:

::: steps
1. The client applies the move immediately and sends it to the server.

2. The server replays the move and acknowledges the resulting position.

3. The client compares that with its prediction and corrects any difference.
:::

When they disagree, the client rewinds to the server's position, replays the moves the server hasn't acknowledged yet, and smooths out the difference over at least `Net.CorrectionSmoothingTime` (0.1 seconds to start). If they're more than `Net.CorrectionThreshold` apart (4 units to start), it's treated as a teleport and snaps straight there.

## Authority

The server has authority. So does a game that isn't connected to anything, like single player. On clients, replicated physics bodies are driven by server updates.

## Not yet supported

There are no RPCs yet, and you can't replicate individual properties or components. Replication currently covers which entities exist (their class, name, parent and scene) and their transforms.
