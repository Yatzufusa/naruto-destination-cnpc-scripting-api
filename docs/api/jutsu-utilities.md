# Jutsu Utilities

Functions for managing jutsu blocks — fire walls, ice blocks, and other terrain created by jutsus.

## Import Statement

```js
var JutsuAPI = Java.type("narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler");
```

## Breaking Jutsu Blocks

### breakJutsuBlocks(npc)

Break all jutsu blocks in a radius of 5 blocks around the NPC, with a 40 tick (2 second) cooldown. Plays particle and sound effects.

```js
JutsuAPI.breakJutsuBlocks(event.npc);
```

---

### breakJutsuBlocks(npc, radius)

Break with a custom radius.

```js
JutsuAPI.breakJutsuBlocks(event.npc, 8);
```

---

### breakJutsuBlocks(npc, radius, cooldown)

Break with custom radius and cooldown (20 ticks = 1 second).

```js
JutsuAPI.breakJutsuBlocks(event.npc, 8, 60); // radius 8, 3 second cooldown
```

---

### breakJutsuBlocks(npc, radius, cooldown, effects)

Full control. Set `effects` to `false` for silent mode (no particles or sound).

```js
JutsuAPI.breakJutsuBlocks(event.npc, 8, 60, false); // silent
```

---

### breakJutsuBlocksSphere(npc, radius, cooldown)

Break in a spherical area instead of a flat radius.

```js
JutsuAPI.breakJutsuBlocksSphere(event.npc, 10, 100);
```

---

### breakJutsuBlocksSphere(npc, radius, cooldown, effects)

Sphere with effect control.

```js
JutsuAPI.breakJutsuBlocksSphere(event.npc, 10, 100, false); // silent sphere
```

---

## Detection

### hasJutsuBlocksNearby(npc, radius)

Returns `true` if there are any jutsu blocks within the given radius.

```js
if (JutsuAPI.hasJutsuBlocksNearby(event.npc, 10)) {
    // there are jutsu blocks nearby
}
```

---

### countJutsuBlocks(npc, radius)

Returns the number of jutsu blocks within the given radius.

```js
var count = JutsuAPI.countJutsuBlocks(event.npc, 10);
event.npc.say("I detect " + count + " jutsu blocks!");
```

---

## Cooldown Management

### isBlockBreakerOnCooldown(npc)

Returns `true` if the block breaker is still on cooldown.

```js
if (!JutsuAPI.isBlockBreakerOnCooldown(event.npc)) {
    JutsuAPI.breakJutsuBlocks(event.npc);
}
```

---

### clearBlockBreakerCooldown(npc)

Manually reset the cooldown.

```js
JutsuAPI.clearBlockBreakerCooldown(event.npc);
```

---

## Effects

### playBlockBreakEffects(npc, x, y, z)

Play smoke/cloud particles and sound at a specific position.

```js
JutsuAPI.playBlockBreakEffects(event.npc, 100, 64, 200);
```

---

### playBlockBreakEffectsAtNpc(npc)

Play effects at the NPC's current position.

```js
JutsuAPI.playBlockBreakEffectsAtNpc(event.npc);
```

---

## Example: Auto-Clear During Combat

Place in the NPC's **Update (Tick)** tab:

```js
var JutsuAPI = Java.type("narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler");

function tick(event) {
    var npc = event.npc;

    // Clear nearby jutsu blocks every 2 seconds during combat
    if (JutsuAPI.hasJutsuBlocksNearby(npc, 6)) {
        JutsuAPI.breakJutsuBlocks(npc, 6, 40);
    }
}
```
