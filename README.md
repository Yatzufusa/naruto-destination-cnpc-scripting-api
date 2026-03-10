# Naruto Destination - CustomNPC+ Scripting API

API documentation for scripting [Naruto Destination](https://www.curseforge.com/minecraft/mc-mods/naruto-destination) NPCs with [CustomNPC+](https://www.curseforge.com/minecraft/mc-mods/custom-npcs).

**Docs:** https://yatzufusa.github.io/naruto-destination-cnpc-scripting-api/

## What is this?

Naruto Destination exposes a scripting API that lets CustomNPC+ NPCs read player stats, cast jutsus, and run scripted boss fights using JavaScript (Nashorn).

This repo hosts the documentation for that API.

## Requirements

- Minecraft 1.7.10 server with Forge
- [Naruto Destination](https://www.curseforge.com/minecraft/mc-mods/naruto-destination)
- [CustomNPC+](https://www.curseforge.com/minecraft/mc-mods/customnpc-plus) (not the original CustomNPC)
- [nashorn.jar](https://www.curseforge.com/minecraft/mc-mods/nashorn-1-7-10/files/2924946)

## Quick Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function interact(event) {
    var player = event.player;
    var rank = stats.getRank(player);
    var nin = stats.getNinjutsu(player);

    if (nin >= 100) {
        player.message("A " + rank + " with " + nin + " Ninjutsu? Prepare yourself!");
    }
}

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        Fireball.cast(event.npc, 30.0, 100);
    }
}
```

## API Overview

| API | What it does |
|---|---|
| **CustomNPCStatsHandler** | Read player stats (level, skills, clan, rank, releases, bijuu, etc.) |
| **Jutsu Classes** | Make NPCs cast projectile jutsus (fireballs, meteors, ice needles, etc.) |
| **CustomNPCJutsuHandler** | All-in-one handler — single import for all jutsus + block breaking |

See the [full documentation](https://yatzufusa.github.io/naruto-destination-cnpc-scripting-api/) for method signatures, examples, and ready-to-use boss scripts.

## Building Docs Locally

```bash
pip install mkdocs-material
mkdocs serve
```
