# Getting Started

## Requirements

- **[Naruto Destination](https://www.curseforge.com/minecraft/mc-mods/naruto-destination)** mod on your server
- **[CustomNPC+](https://www.curseforge.com/minecraft/mc-mods/customnpc-plus)** mod on your server (not the original CustomNPC)
- **[nashorn.jar](https://www.curseforge.com/minecraft/mc-mods/nashorn-1-7-10/files/2924946)** in your `mods` folder — adds JavaScript scripting to CustomNPC+

If you don't see a scripting language option in the NPC scripting tab, you're missing nashorn.

## The Three APIs

| API | Import | What it does |
|---|---|---|
| **Stats Handler** | `narutodestination.Mathioks.CNPC.CustomNPCStatsHandler` | Read player stats |
| **Jutsu Classes** | `narutodestination.Mathioks.CNPC.Jutsus.*` | Make NPCs cast jutsus |
| **Jutsu Handler** | `narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler` | Break jutsu blocks, play effects |

## Writing a Script

1. Open an NPC's settings in CustomNPC+
2. Go to the **Scripting** tab
3. Select **ECMAScript** as the language
4. Pick the right event tab:
    - **Interact** — when a player right-clicks the NPC
    - **Update (Tick)** — every tick (20x per second) — put combat jutsus here
    - **Init** — once when the NPC spawns

### Reading Player Stats

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;
    var level = stats.getLevel(player);

    if (level >= 50) {
        player.message("You are strong enough to enter.");
    } else {
        player.message("Come back when you're level 50.");
    }
}
```

### Casting Jutsus

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        Fireball.cast(event.npc);
    }
}
```

## Return Types

| Type | Example |
|---|---|
| `int` | Skill levels, points, IDs |
| `boolean` | Clan checks, ability unlocks |
| `String` | Clan name, rank, mangekyou variant |
| `double` | Bijuu unlock progress |
| `String[]` | Known releases, known clans |

## Common Patterns

### Gate content behind rank

Rank IDs are strings like `"Genin"`, `"Chunin"`, `"Jonin"`, `"Kage"`, etc.

```js
var rank = stats.getRank(event.player);
if (rank == "Jonin" || rank == "Kage") {
    event.player.message("Welcome, " + rank + ".");
} else {
    event.player.message("Only Jonin and above may enter.");
}
```

### Check nature release

Nature releases are `0` (don't have it) or `1` (have it):

```js
if (stats.getFireRelease(event.player) > 0) {
    event.player.message("You know Fire Release!");
}
```

### Check clan

```js
if (stats.hasUchihaClan(event.player)) {
    event.player.message("Welcome, Uchiha.");
}
```

### Loop through arrays

```js
var releases = stats.getKnownReleases(event.player);
for (var i = 0; i < releases.length; i++) {
    event.player.message("You know: " + releases[i]);
}
```
