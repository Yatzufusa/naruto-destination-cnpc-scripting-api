# Naruto Destination - CustomNPC+ Scripting API

!!! warning "This API is for CustomNPC+, not the original CustomNPC"
    Make sure you have the correct version installed. The original/default CustomNPC mod does not support this.

This API lets CustomNPC+ NPCs interact with the Naruto Destination mod — reading player stats, casting jutsus, and building scripted boss fights.

## Quick Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function interact(event) {
    var player = event.player;
    var ninjutsu = stats.getNinjutsu(player);
    var rank = stats.getRank(player);

    if (ninjutsu >= 100) {
        player.message("A " + rank + " with " + ninjutsu + " Ninjutsu? Prepare yourself!");
    } else {
        player.message("Train your Ninjutsu and come back.");
    }
}

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        Fireball.cast(event.npc, 30.0, 100);
    }
}
```

## Player Stats

| Page | |
|---|---|
| [General Stats](api/general-stats.md) | Level, skill points, jutsu points, intelligence |
| [Skills](api/skills.md) | Ninjutsu, Taijutsu, Genjutsu, and the other combat skills |
| [Chakra & Health](api/chakra-health.md) | Chakra pool, health stat, health caps |
| [Clan & Affiliation](api/clan-affiliation.md) | Clan, rank, village, land |
| [Nature Releases](api/nature-releases.md) | Fire, Water, Wind, Earth, Lightning, Yin, Yang |
| [Kekkei Genkai](api/kekkei-genkai.md) | Wood, Lava, Ice, Sharingan, Byakugan, etc. |
| [Clan Checks](api/clan-checks.md) | Boolean clan membership checks |
| [Bijuu](api/bijuu.md) | Tailed beast type, unlock progress, scale |
| [Abilities](api/abilities.md) | Sage Mode, Susanoo, Curse Seal, Eight Gates, etc. |
| [Helpers](api/helpers.md) | Arrays of known releases, clans, bijuu |

## NPC Jutsus

| Page | |
|---|---|
| [Standard Jutsus](api/jutsus.md) | Fireballs, meteors, water bullets, and 12 more |
| [Continuous Jutsus](api/continuous-jutsus.md) | Jutsus that fire over time (Magnet Gold Push) |
| [Jutsu Utilities](api/jutsu-utilities.md) | Breaking jutsu blocks, detection, effects |

## Guides

| Page | |
|---|---|
| [Getting Started](getting-started.md) | Setup, imports, first script |
| [Script Examples](examples.md) | Full boss scripts, multi-element NPCs, phase transitions |
| [Tips & Troubleshooting](tips.md) | Cooldowns, debugging, common issues |
