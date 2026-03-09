# Chakra & Health

## Chakra

### getCurrentChakra
```js
int stats.getCurrentChakra(player)
```
Current chakra.

---

### getMaxChakra
```js
int stats.getMaxChakra(player)
```
Max chakra capacity.

---

## Health

These are the Naruto Destination health values, not vanilla Minecraft hearts.

### getHealth
```js
int stats.getHealth(player)
```
Current health stat.

---

### getHealthCap
```js
int stats.getHealthCap(player)
```
Base health cap.

---

### getHealthOtsuCap
```js
int stats.getHealthOtsuCap(player)
```
Otsutsuki health cap bonus.

---

### getHealthTBCap
```js
int stats.getHealthTBCap(player)
```
Tailed Beast health cap bonus.

---

## Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;
    var chakra = stats.getCurrentChakra(player);
    var maxChakra = stats.getMaxChakra(player);
    var percent = Math.floor((chakra / maxChakra) * 100);

    player.message("Chakra: " + chakra + "/" + maxChakra + " (" + percent + "%)");
}
```
