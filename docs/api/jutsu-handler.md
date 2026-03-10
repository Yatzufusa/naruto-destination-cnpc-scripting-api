# Jutsu Handler (All-in-One)

Instead of importing each jutsu class separately, you can import `CustomNPCJutsuHandler` and call everything through it.

```js
var jutsu = Java.type("narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler");
```

This one import gives you access to all standard jutsus, Magnet Push, and jutsu block breaking.

## Standard Jutsus

Every standard jutsu has the same three method patterns. Using fireball as an example:

```js
jutsu.fireball(npc)                      // default damage + cooldown
jutsu.fireball(npc, 50.0)               // custom damage
jutsu.fireball(npc, 50.0, 100)          // custom damage + cooldown (20 ticks = 1 sec)
jutsu.fireballPercent(npc, 5.0, 0.5)    // 5 base + 50% of target's max HP
jutsu.fireballPercent(npc, 5.0, 0.5, 60) // same with custom cooldown
```

All return `boolean` — `true` if the jutsu was cast, `false` if it was on cooldown.

### Available Methods

| Jutsu | Method Name | Description |
|---|---|---|
| Fireball | `fireball` / `fireballPercent` | Large fireball projectile |
| Fire Bullet | `fireBullet` / `fireBulletPercent` | Explosive fire bullet |
| Water Bullet | `waterBullet` / `waterBulletPercent` | Triple water bullet barrage (3x damage in water) |
| Lightning Ball | `lightningBall` / `lightningBallPercent` | Electric projectile with stun + AOE in water |
| Meteor | `meteor` / `meteorPercent` | Massive meteor from the sky (Tengai) |
| Boil Meltdown | `boilMeltdown` / `boilMeltdownPercent` | Explosive projectile with fire + poison |
| Crystal Dragon | `crystalDragon` / `crystalDragonPercent` | Crystal dragon projectile |
| Dust Cube | `dustCube` / `dustCubePercent` | Particle style cube explosion |
| Clay Birds | `clayBirds` / `clayBirdsPercent` | C1 explosive clay birds |
| Lava Rock | `lavaRock` / `lavaRockPercent` | Lava rock with fire spread |
| Ice Needles | `iceNeedles` / `iceNeedlesPercent` | 9 ice needles in spread pattern |
| Storm Demon | `stormDemon` / `stormDemonPercent` | Storm cloud with AOE damage + slowness |
| Scorch Ring | `scorchRing` / `scorchRingPercent` | 4 homing fireballs with fire + weakness |
| Steel Projectile | `steelProjectile` / `steelProjectilePercent` | Steel projectile |
| Wood Dragon | `woodDragon` / `woodDragonPercent` | Wood dragon with explosion + slowness |

---

## Magnet Gold Push (Continuous)

Continuous jutsu — fires gold dust repeatedly for a short burst. Needs `magnetPushUpdate()` called every tick.

### magnetPush(npc) / magnetPush(npc, damage) / magnetPush(npc, damage, cooldown)

Start the jutsu.

```js
jutsu.magnetPush(event.npc);
jutsu.magnetPush(event.npc, 8.0);
jutsu.magnetPush(event.npc, 8.0, 60);
```

### magnetPushPercent(npc, base, percent) / magnetPushPercent(npc, base, percent, cooldown)

Start with percentage-based damage.

```js
jutsu.magnetPushPercent(event.npc, 5.0, 0.3); // 5 base + 30% of target max HP
```

### magnetPushUpdate(npc)

**Must be called every tick.** Without this, the jutsu won't fire.

```js
jutsu.magnetPushUpdate(event.npc);
```

### magnetPushIsActive(npc)

Returns `true` if the jutsu is currently firing.

### magnetPushStop(npc)

Force stop the jutsu.

---

## Jutsu Block Breaking

Same methods as the [Jutsu Utilities](jutsu-utilities.md) page, accessible through the handler.

```js
jutsu.breakJutsuBlocks(npc)                          // defaults: radius 5, cooldown 40, effects on
jutsu.breakJutsuBlocks(npc, radius)
jutsu.breakJutsuBlocks(npc, radius, cooldown)
jutsu.breakJutsuBlocks(npc, radius, cooldown, false)  // silent (no effects)
jutsu.breakJutsuBlocksSphere(npc, radius, cooldown)
jutsu.breakJutsuBlocksSphere(npc, radius, cooldown, false)

jutsu.hasJutsuBlocksNearby(npc, radius)   // boolean
jutsu.countJutsuBlocks(npc, radius)       // int

jutsu.isBlockBreakerOnCooldown(npc)       // boolean
jutsu.clearBlockBreakerCooldown(npc)

jutsu.playBlockBreakEffects(npc, x, y, z)
jutsu.playBlockBreakEffectsAtNpc(npc)
```

---

## Example: Multi-Jutsu Boss

Using the handler you only need one import for everything:

```js
var jutsu = Java.type("narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler");

function init(event) {
    event.npc.setStoredData("phase", 1);
}

function tick(event) {
    var npc = event.npc;
    var target = npc.getAttackTarget();
    jutsu.magnetPushUpdate(npc);

    if (target == null) return;

    var hp = npc.getHealth() / npc.getMaxHealth();

    // Phase transition at 50% HP
    if (hp < 0.5 && npc.getStoredData("phase") < 2) {
        npc.setStoredData("phase", 2);
        npc.say("\u00a75You've pushed me this far...");
    }

    // Clear jutsu blocks
    if (jutsu.hasJutsuBlocksNearby(npc, 6)) {
        jutsu.breakJutsuBlocks(npc, 6, 40);
    }

    // Attack based on phase
    var phase = npc.getStoredData("phase");
    var random = Math.random();

    if (phase >= 2) {
        if (random < 0.3) {
            jutsu.meteor(npc, 50.0, 300);
        } else if (random < 0.6) {
            jutsu.fireballPercent(npc, 10.0, 0.3, 60);
        } else {
            jutsu.magnetPush(npc, 8.0, 40);
        }
    } else {
        jutsu.fireball(npc, 25.0, 100);
    }
}
```

## Handler vs Individual Imports

Both approaches work the same. The handler just saves you imports.

**Handler (one import):**
```js
var jutsu = Java.type("narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler");
jutsu.fireball(event.npc, 30.0);
jutsu.meteor(event.npc, 50.0);
```

**Individual classes (one import per jutsu):**
```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");
var Tengai = Java.type("narutodestination.Mathioks.CNPC.Jutsus.TengaiJutsu");
Fireball.cast(event.npc, 30.0);
Tengai.cast(event.npc, 50.0);
```

Use whichever you prefer. The individual classes use `cast()` / `percent()`, the handler uses the jutsu name directly.
