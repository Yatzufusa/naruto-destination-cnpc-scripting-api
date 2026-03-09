# Script Examples

Ready-to-use scripts. All go in the NPC's **Update (Tick)** tab unless noted otherwise.

## Madara Boss (Full Multi-Phase Fight)

A boss NPC that throws fireballs, switches to a harder phase at 50% HP, and drops a meteor after every few fireballs.

**Init Tab:**

```js
event.npc.setStoredData("fireballCount", 0);
event.npc.setStoredData("phase", 1);
event.npc.setTitle("\u00a74[Madara Uchiha]");
```

**Update Tab:**

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");
var Tengai = Java.type("narutodestination.Mathioks.CNPC.Jutsus.TengaiJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target == null) return;

    var hp = event.npc.getHealth() / event.npc.getMaxHealth();
    var currentPhase = event.npc.hasStoredData("phase")
        ? event.npc.getStoredData("phase") : 1;

    // Phase 2 at 50% HP
    if (hp < 0.5 && currentPhase < 2) {
        event.npc.setStoredData("phase", 2);
        event.npc.say("\u00a75\u00a7l\u00a7nYou've forced me to get serious!");
        event.npc.setTitle("\u00a74[Madara Uchiha - Phase 2]");
    }

    var fireballCount = event.npc.hasStoredData("fireballCount")
        ? event.npc.getStoredData("fireballCount") : 0;

    var fireballCooldown = currentPhase >= 2 ? 50 : 100;
    var fireballsNeeded = currentPhase >= 2 ? 3 : 5;

    // Drop a meteor after X fireballs
    if (fireballCount >= fireballsNeeded) {
        var tengaiDamage = currentPhase >= 2 ? 100.0 : 75.0;
        if (Tengai.cast(event.npc, tengaiDamage, 600)) {
            event.npc.say("\u00a75\u00a7l\u00a7nTENGAI SHINSEI!");
            event.npc.setStoredData("fireballCount", 0);
        }
    }

    // Spam fireballs
    var fireballDamage = currentPhase >= 2 ? 45.0 : 30.0;
    if (Fireball.cast(event.npc, fireballDamage, fireballCooldown)) {
        event.npc.say("\u00a7c\u00a7lFireball Jutsu!");
        event.npc.setStoredData("fireballCount", fireballCount + 1);
    }
}
```

---

## HP-Based Jutsu Scaling

An NPC that gets more dangerous as it loses health.

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function tick(event) {
    var target = event.npc.getAttackTarget();
    if (target == null) return;

    var hp = event.npc.getHealth() / event.npc.getMaxHealth();

    if (hp < 0.25) {
        // Desperation: percentage damage
        Fireball.percent(event.npc, 10.0, 0.8, 40); // 10 + 80% of target HP
    } else if (hp < 0.50) {
        // Phase 2: stronger and faster
        Fireball.cast(event.npc, 50.0, 60);
    } else {
        // Phase 1: normal attacks
        Fireball.cast(event.npc, 30.0, 100);
    }
}
```

---

## Smart AI with Distance Check

An NPC that picks jutsus based on distance to its target.

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");
var Tengai = Java.type("narutodestination.Mathioks.CNPC.Jutsus.TengaiJutsu");
var IceNeedles = Java.type("narutodestination.Mathioks.CNPC.Jutsus.IceReleaseIceNeedlesJutsu");

function tick(event) {
    var npc = event.npc;
    var target = npc.getAttackTarget();
    if (target == null) return;

    var distance = npc.getPos().distanceTo(target.getPos());
    var hp = npc.getHealth() / npc.getMaxHealth();

    if (hp < 0.3) {
        // Desperation: meteor
        Tengai.cast(npc, 80.0, 200);
    } else if (distance > 15) {
        // Long range: fireball
        Fireball.cast(npc, 30.0, 80);
    } else {
        // Close range: ice needles spread
        IceNeedles.cast(npc, 15.0, 60);
    }
}
```

---

## Environmental Awareness

An NPC that adapts its jutsus based on the environment.

```js
var WaterBullet = Java.type("narutodestination.Mathioks.CNPC.Jutsus.WaterBulletJutsu");
var LightningBall = Java.type("narutodestination.Mathioks.CNPC.Jutsus.LightningBallJutsu");
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function tick(event) {
    var npc = event.npc;
    var target = npc.getAttackTarget();
    if (target == null) return;

    // Check if NPC is in water
    if (npc.getMCEntity().isInWater()) {
        LightningBall.cast(npc, 30.0); // AOE damage in water
        return;
    }

    // Check if target is in water
    if (target.getMCEntity().isInWater()) {
        WaterBullet.cast(npc, 20.0); // 3x damage when target is in water
        return;
    }

    // Default: fireball
    Fireball.cast(npc, 25.0);
}
```

---

## Stat-Gated NPC Trainer

An NPC that checks the player's stats and gives different responses.

Place in the **Interact** tab:

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;
    var nin = stats.getNinjutsu(player);
    var rank = stats.getRank(player);
    var level = stats.getLevel(player);

    if (level < 20) {
        player.message("You're too inexperienced. Come back at level 20.");
        return;
    }

    if (nin < 50) {
        player.message("Your Ninjutsu is only " + nin + ". Train more.");
        return;
    }

    var releases = stats.getKnownReleases(player);
    player.message("Welcome, " + rank + "! You know " + releases.length + " releases.");
    player.message("You are ready for advanced training.");
}
```

---

## Clan-Specific Dialogue

Place in the **Interact** tab:

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;

    if (stats.hasUchihaClan(player)) {
        var sharingan = stats.getSharinganSize(player);
        if (sharingan >= 4) {
            player.message("Your Mangekyou... it carries a heavy burden.");
        } else if (sharingan > 0) {
            player.message("Those eyes... you are of the Uchiha.");
        } else {
            player.message("Uchiha blood, but your Sharingan hasn't awakened yet.");
        }
    } else if (stats.hasHyugaClan(player)) {
        player.message("The Byakugan sees all. Welcome, Hyuga.");
    } else if (stats.hasSenjuClan(player)) {
        player.message("Descendant of Hashirama... impressive lineage.");
    } else {
        player.message("Greetings, shinobi.");
    }
}
```

---

## Jutsu Block Clearing Boss

A boss that clears jutsu terrain around itself while fighting.

```js
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");
var JutsuAPI = Java.type("narutodestination.Mathioks.CNPC.CustomNPCJutsuHandler");

function tick(event) {
    var npc = event.npc;
    var target = npc.getAttackTarget();

    // Clear any jutsu blocks nearby
    if (JutsuAPI.hasJutsuBlocksNearby(npc, 6)) {
        JutsuAPI.breakJutsuBlocks(npc, 6, 40);
    }

    // Attack target
    if (target != null) {
        Fireball.cast(npc, 35.0, 80);
    }
}
```

---

## Continuous Jutsu + Standard Jutsu Combo

A Gaara-style NPC that uses both continuous and standard jutsus.

```js
var MagnetPush = Java.type("narutodestination.Mathioks.CNPC.Jutsus.MagnetGoldPushJutsu");
var Fireball = Java.type("narutodestination.Mathioks.CNPC.Jutsus.FireballJutsu");

function tick(event) {
    var npc = event.npc;
    var target = npc.getAttackTarget();

    // Always update continuous jutsus
    MagnetPush.update(npc);

    if (target == null) return;

    var hp = npc.getHealth() / npc.getMaxHealth();

    if (hp < 0.5) {
        // Low HP: use magnet push
        if (!MagnetPush.isActive(npc)) {
            MagnetPush.activate(npc, 8.0, 40);
        }
    } else {
        // Full HP: use fireballs
        Fireball.cast(npc, 25.0, 80);
    }
}
```
