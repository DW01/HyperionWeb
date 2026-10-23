---
title: Play-in-editor
description: Play your game inside the Hyperion editor, including as a client or dedicated server for multiplayer testing.
lede: Run your game inside the editor, without making a separate build.
summary: Run the game in the editor, standalone or networked.
---

## Play, pause, stop

The :icon[play] **Play**, :icon[debug-pause] **Pause** and :icon[debug-stop] **Stop** buttons are near the right end of the toolbar.

Play saves your project first, and Stop restores that saved state, so changes made while playing are discarded. A project that's never been saved asks you to save it before playing.

**Ghost Mode** (in the :icon[settings-gear] gear menu) gives you a free camera while playing. Move it with <kbd>W</kbd> <kbd>A</kbd> <kbd>S</kbd> <kbd>D</kbd>, <kbd>Space</kbd> and <kbd>Ctrl</kbd>.

## Network modes

Pick a mode from the :icon[chevron-down] arrow next to **Play**. The option you select will be saved as the default play mode for next time.

| Mode | Play button action |
|---|---|
| Play Local | The game runs in the editor in single player |
| Play as Client | The editor connects to the server at **Host**:**Port**. Start the server first, separately; see [Running a server](/docs/multiplayer/server.html). |
| Play as Dedicated Server | The editor hosts the game on **Port**. It has no player of its own; players spawn for clients that connect. |

**Stop** disconnects or stops hosting.

The same menu has **Play in Web Browser**, which builds the game for the web and opens it in your browser. See [Web](/docs/platforms/web.html).

:::note
Nothing is replicated unless the game's world has the `IsReplicated` flag. It's part of the world's default flags, so a world saved with `Flags = Default` has it.
But it is something to look into if you're having issues in this area. On your filesystem, open your project's `Content/Worlds/MainWorld.hmf` file and look at its `Flags`.
:::

### Network Settings

Open **Network Settings...** from the same menu.

| Setting | Default | Used for |
|---|---|---|
| Host | `127.0.0.1` | The server Play as Client connects to |
| Port | `9192` | The game server port, in both networked modes |
| Cache Server Port | `8081` | In Play as Dedicated Server, serves your saved project to clients that connect |

### More players

When the editor plays as a dedicated server, run the game against it to add players, syncing content from the editor's cache server:

```shell
hyperion-sample --host=127.0.0.1 --gameport=9192 --cacheserver=http://127.0.0.1:8081
```
