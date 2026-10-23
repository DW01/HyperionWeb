---
title: Running a server
description: Run a Hyperion Engine dedicated server from the command line and connect clients to it.
lede: Starting a dedicated server
summary: Starting a dedicated server
---

## Start a server

The game executable runs as a server with `--server`:

```shell
hyperion-sample --server --gameport=9192
```

It runs headless (no window), and reads console commands from its terminal. Leave off `--gameport` and it uses the `Net.GameServerPort` CVar, which defaults to 9192. A headless server ticks at up to 60 times a second, set with `Sim.HeadlessTickRate`.

Add `--startupworld=<WorldName>` to pick the world it starts in.

## Connect a client

Run the game executable with `--host` to connect to the server at that address:

```shell
hyperion-sample --host=127.0.0.1 --gameport=9192
```

With `--autoconnect=false`, or without `--host`, it shows a screen where you can change the address before connecting, or pick Single Player instead.

## Your own game

A game [built from the editor](/docs/editor/build-game.html) takes the same flags. It starts in single player by default, because its `Config/GlobalConfig.json` passes `--singleplayer`. Pass `--singleplayer=false` to override it.

For example:

```shell
MyGame --server # start standalone a server
MyGame --singleplayer=false --host=127.0.0.1 # connect to a server
```

## From the editor

The editor can start a local server and connect to it for play-in-editor with networking. See [play-in-editor](/docs/editor/play-in-editor.html) for info
