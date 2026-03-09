# Continuous Jutsus

Unlike [standard jutsus](jutsus.md), these fire continuously over time and require calling `update()` **every tick**.

## Available Continuous Jutsus

| Jutsu | Import Name | Description |
|---|---|---|
| Magnet Gold Push | `MagnetGoldPushJutsu` | Rapid-fire gold dust for 0.5 seconds |

## Import Statement

```js
var MagnetPush = Java.type("narutodestination.Mathioks.CNPC.Jutsus.MagnetGoldPushJutsu");
```

## Methods

### activate(npc)

Start the jutsu with default damage and cooldown.

```js
MagnetPush.activate(event.npc);
```

---

### activate(npc, damage)

Start with custom damage.

```js
MagnetPush.activate(event.npc, 10.0);
```

---

### activate(npc, damage, cooldown)

Start with custom damage and cooldown.

```js
MagnetPush.activate(event.npc, 10.0, 60);
```

---

### update(npc)

**Must be called every tick** in the Update tab for the jutsu to work. Without this call, it won't fire.

```js
MagnetPush.update(event.npc);
```

---

### isActive(npc)

Check if the jutsu is currently firing. Returns `boolean`.

```js
if (MagnetPush.isActive(event.npc)) {
    // jutsu is running
}
```

---

### deactivate(npc)

Force stop the jutsu before it finishes naturally.

```js
MagnetPush.deactivate(event.npc);
```

---

## Example: Gaara-Style Sand Ninja

Place in the NPC's **Update (Tick)** tab:

```js
var MagnetPush = Java.type("narutodestination.Mathioks.CNPC.Jutsus.MagnetGoldPushJutsu");

function tick(event) {
    var npc = event.npc;
    var target = npc.getAttackTarget();

    // ALWAYS call update() - this makes the jutsu work
    MagnetPush.update(npc);

    if (target != null && !MagnetPush.isActive(npc)) {
        if (MagnetPush.activate(npc, 5.0)) {
            npc.say("Magnet Release: Gold Push!");
        }
    }
}
```

Always call `update()` at the top of your tick function, before any activation logic — that way the jutsu keeps running even if your other conditions change.
