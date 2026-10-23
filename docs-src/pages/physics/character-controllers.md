---
title: Character controllers
description: Use the character controller component in Hyperion Engine for player movement: movement and jump settings, input, and network prediction.
lede: The character controller handles walking, running and jumping, with collision against the world.
summary: Walking, running and jumping.
---

## Adding one

Add a `CharacterControllerComponent` to an entity. By default it's driven by keyboard input:

| Action | Key |
|---|---|
| Move | <kbd>W</kbd> <kbd>A</kbd> <kbd>S</kbd> <kbd>D</kbd> |
| Sprint | <kbd>Shift</kbd> |
| Jump | <kbd>Space</kbd> |

`isOnGround` is true while it's standing on something, including slopes too steep to walk up.

## Movement settings

These are under `movement`:

| Setting | What it does |
|---|---|
| moveSpeed | Walking speed, in m/s. Starts at 15. |
| sprintSpeed | Running speed. Starts at 25. |
| groundAcceleration, airAcceleration | How quickly it gets up to speed on the ground, and how much it can steer in the air. |
| friction | How quickly it slows down when you let go. |
| stepHeight | The tallest step it can walk straight up. Starts at 0.35. |
| maxSlopeAngle | The steepest slope it can walk up, in degrees. Starts at 55. |
| orientToMovement | Turns the character to face the way it's moving, at `turnRate` degrees per second. |

On slopes steeper than `maxSlopeAngle`, the character slides down, and can still jump off, pushed away from the slope.

## Jump settings

These are under `jump`:

| Setting | What it does |
|---|---|
| speed | Initial jump speed. Starts at 4.9. |
| coyoteTime | Grace period for jumping after leaving a ledge. Starts at 0.15 seconds. |
| bufferTime | How early before landing a jump press still counts. Starts at 0.15 seconds. |
| cutGravityMultiplier | Extra gravity while rising if you let go of jump early, for variable jump height. |
| apexGravityMultiplier, fallGravityMultiplier | Gravity near the top of the jump (below 1 gives a little hang time), and while falling. |

## Pushing things

Under `push`, `massLimit` is the heaviest dynamic body the character can push (350 to start), and `maxSpeed` caps how fast it pushes it.

## In multiplayer

The local player's movement is predicted on the client, so input responds immediately. The server validates each move and corrects the client if they disagree. More in [replication](/docs/multiplayer/replication.html).
