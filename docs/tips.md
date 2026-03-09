# Tips & Troubleshooting

## Pro Tips

### Cooldowns

- Cooldowns are **per-jutsu**, not global — an NPC can have multiple jutsus cooling down at the same time
- NPCs can cast different jutsus simultaneously
- **20 ticks = 1 second**
- Use longer cooldowns for powerful jutsus to keep fights balanced

### Percentage Damage

Great for bosses that need to challenge players regardless of their health pool:

```js
// Deals 10 + 50% of target's max HP
Fireball.percent(event.npc, 10.0, 0.5);
```

- Scales automatically with the target's health
- Keeps bosses challenging for both low and high HP players
- Combine a low base damage with a high percent for consistent threat

### Cast Returns Boolean

`cast()` and `activate()` return `true` if the jutsu was actually fired (not on cooldown). Use this for dialogue or effects:

```js
if (Fireball.cast(event.npc, 30.0, 100)) {
    event.npc.say("Fire Style: Fireball Jutsu!");
}
```

### Stored Data for State

Use `setStoredData` / `getStoredData` to track NPC state across ticks:

```js
// Init tab
event.npc.setStoredData("phase", 1);
event.npc.setStoredData("attackCount", 0);

// Update tab
var phase = event.npc.getStoredData("phase");
var count = event.npc.getStoredData("attackCount");
```

### Distance-Based AI

Make NPCs pick different jutsus based on range:

```js
var target = event.npc.getAttackTarget();
if (target != null) {
    var distance = event.npc.getPos().distanceTo(target.getPos());

    if (distance > 15) {
        // long range
    } else {
        // close range
    }
}
```

### Environmental Checks

```js
// Check if NPC is in water
if (event.npc.getMCEntity().isInWater()) {
    // use water/lightning jutsus
}

// Check if target is in water
if (target.getMCEntity().isInWater()) {
    // WaterBullet does 3x damage, LightningBall does AOE
}
```

---

## Common Issues

### Jutsu not firing

- Make sure the NPC has a target: `event.npc.getAttackTarget()` returns `null` if there's no target
- Check if the cooldown has expired — if you cast the same jutsu too fast, it silently skips
- Use `event.npc.say("debug")` to check whether your code is actually running
- Make sure the script is in the **Update (Tick)** tab, not the Interact tab

### No damage dealt

- Make sure the damage value is greater than 0
- Check if the target has invulnerability frames
- Verify the projectile is spawning (add a `say()` after `cast()`)

### Continuous jutsu not working

- You **must** call `update()` every tick — put it at the top of your tick function
- Call `update()` even when there's no target, so an active jutsu can keep running

### No scripting language available

You need **[nashorn.jar](https://www.curseforge.com/minecraft/mc-mods/nashorn-1-7-10/files/2924946)** in your server's `mods` folder. This adds the JavaScript (ECMA) scripting language to CustomNPC+.

### Scripts not running at all

Make sure you have **CustomNPC+** installed, not the original CustomNPC. This API only works with the updated fork.
