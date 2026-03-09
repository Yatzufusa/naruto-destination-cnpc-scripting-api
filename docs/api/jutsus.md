# Standard Jutsus

Each jutsu is a separate class with the same set of methods. All go in the NPC's **Update (Tick)** tab.

## Available Jutsus

| Jutsu | Import Name | Description |
|---|---|---|
| Fireball | `FireballJutsu` | Large fireball projectile |
| Fire Bullet | `FireBulletJutsu` | Explosive fire bullet |
| Water Bullet | `WaterBulletJutsu` | Triple water bullet barrage (3x damage in water) |
| Lightning Ball | `LightningBallJutsu` | Electric projectile with stun + AOE in water |
| Tengai | `TengaiJutsu` | Massive meteor from the sky |
| Boil Meltdown | `BoilReleaseMeltdownJutsu` | Explosive projectile with fire + poison |
| Crystal Dragon | `CrystalDragonJutsu` | Crystal dragon projectile |
| Dust Cube | `DustAtomicDismantlingCubeJutsu` | Particle style cube explosion |
| Explosive Clay Birds | `ExplosiveClayBirdsJutsu` | C1 explosive clay birds |
| Lava Rock | `LavaReleaseStreamRockJutsu` | Lava rock with fire spread |
| Ice Needles | `IceReleaseIceNeedlesJutsu` | 9 ice needles in spread pattern |
| Storm Demon | `StormReleaseDemonJutsu` | Storm cloud with AOE damage + slowness |
| Scorch Ring | `ScorchReleaseRingOfSunsJutsu` | 4 homing fireballs with fire + weakness |
| Steel Projectile | `SteelReleaseProjectileJutsu` | Steel projectile |
| Wood Dragon | `WoodDragonJutsu` | Wood dragon with explosion + slowness |

## Import Statements

Each jutsu is imported separately. Only import the ones you need:

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");
var FireBullet = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireBulletJutsu");
var WaterBullet = Java.type("narutodestination.Mathioks.CNPC.Jutsus.WaterBulletJutsu");
var LightningBall = Java.type("narutodestination.Mathioks.CNPC.Jutsus.LightningBallJutsu");
var Tengai = Java.type("narutodestination.Mathioks.CNPC.Jutsus.TengaiJutsu");
var BoilMeltdown = Java.type("narutodestination.Mathioks.CNPC.Jutsus.BoilReleaseMeltdownJutsu");
var CrystalDragon = Java.type("narutodestination.Mathioks.CNPC.Jutsus.CrystalDragonJutsu");
var DustCube = Java.type("narutodestination.Mathioks.CNPC.Jutsus.DustAtomicDismantlingCubeJutsu");
var ClayBirds = Java.type("narutodestination.Mathioks.CNPC.Jutsus.ExplosiveClayBirdsJutsu");
var LavaRock = Java.type("narutodestination.Mathioks.CNPC.Jutsus.LavaReleaseStreamRockJutsu");
var IceNeedles = Java.type("narutodestination.Mathioks.CNPC.Jutsus.IceReleaseIceNeedlesJutsu");
var StormDemon = Java.type("narutodestination.Mathioks.CNPC.Jutsus.StormReleaseDemonJutsu");
var ScorchRing = Java.type("narutodestination.Mathioks.CNPC.Jutsus.ScorchReleaseRingOfSunsJutsu");
var SteelProjectile = Java.type("narutodestination.Mathioks.CNPC.Jutsus.SteelReleaseProjectileJutsu");
var WoodDragon = Java.type("narutodestination.Mathioks.CNPC.Jutsus.WoodDragonJutsu");
```

## Methods

Every standard jutsu has the same five methods. The examples below use `Fireball`, but they work the same for all jutsus listed above.

### cast(npc)

Cast with default damage and cooldown.

```js
Fireball.cast(event.npc);
```

---

### cast(npc, damage)

Cast with custom damage, default cooldown.

```js
Fireball.cast(event.npc, 50.0);
```

---

### cast(npc, damage, cooldownTicks)

Cast with custom damage and cooldown. 20 ticks = 1 second.

```js
Fireball.cast(event.npc, 50.0, 100); // 50 damage, 5 second cooldown
```

---

### percent(npc, baseDamage, percentHP)

Cast with percentage-based damage. Final damage = `baseDamage + (percentHP * target's max HP)`.

```js
Fireball.percent(event.npc, 5.0, 0.5); // 5 + 50% of target's max HP
```

---

### percent(npc, baseDamage, percentHP, cooldownTicks)

Percentage damage with custom cooldown.

```js
Fireball.percent(event.npc, 5.0, 0.5, 60); // 3 second cooldown
```

---

## Examples

### Basic fire NPC

Place in the NPC's **Update (Tick)** tab:

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        Fireball.cast(event.npc);
    }
}
```

### Water ninja with custom damage

```js
var WaterBullet = Java.type("narutodestination.Mathioks.CNPC.Jutsus.WaterBulletJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        WaterBullet.cast(event.npc, 25.0, 200);
    }
}
```

WaterBullet automatically does 3x damage when the NPC is in water.

### Homing projectiles

```js
var ScorchRing = Java.type("narutodestination.Mathioks.CNPC.Jutsus.ScorchReleaseRingOfSunsJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        if (ScorchRing.cast(event.npc, 15.0)) {
            event.npc.say("Scorch Release: Ring of Suns!");
        }
    }
}
```

ScorchRing spawns 4 homing fireballs that track the target.

### Random jutsu selection

```js
var BoilMeltdown = Java.type("narutodestination.Mathioks.CNPC.Jutsus.BoilReleaseMeltdownJutsu");
var LavaRock = Java.type("narutodestination.Mathioks.CNPC.Jutsus.LavaReleaseStreamRockJutsu");
var StormDemon = Java.type("narutodestination.Mathioks.CNPC.Jutsus.StormReleaseDemonJutsu");
var IceNeedles = Java.type("narutodestination.Mathioks.CNPC.Jutsus.IceReleaseIceNeedlesJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        var random = Math.random();

        if (random < 0.25) {
            BoilMeltdown.cast(event.npc, 20.0);
        } else if (random < 0.50) {
            LavaRock.cast(event.npc, 20.0);
        } else if (random < 0.75) {
            StormDemon.cast(event.npc, 10.0);
        } else {
            IceNeedles.cast(event.npc, 8.0);
        }
    }
}
```

### Percentage damage boss

```js
var DustCube = Java.type("narutodestination.Mathioks.CNPC.Jutsus.DustAtomicDismantlingCubeJutsu");
var ScorchRing = Java.type("narutodestination.Mathioks.CNPC.Jutsus.ScorchReleaseRingOfSunsJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target != null) {
        var random = Math.random();

        if (random < 0.3) {
            // 10 base + 20% of target's max HP
            DustCube.percent(event.npc, 10.0, 0.20);
        } else {
            // 5 base + 10% of target's max HP
            ScorchRing.percent(event.npc, 5.0, 0.10);
        }
    }
}
```
