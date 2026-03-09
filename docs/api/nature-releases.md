# Nature Releases

All return `int` — `0` means the player doesn't have it, `1` means they do.

## getFireRelease
```js
int stats.getFireRelease(player)
```

---

## getWaterRelease
```js
int stats.getWaterRelease(player)
```

---

## getWindRelease
```js
int stats.getWindRelease(player)
```

---

## getEarthRelease
```js
int stats.getEarthRelease(player)
```

---

## getLightningRelease
```js
int stats.getLightningRelease(player)
```

---

## getYinRelease
```js
int stats.getYinRelease(player)
```

---

## getYangRelease
```js
int stats.getYangRelease(player)
```

---

## getYinYangRelease
```js
int stats.getYinYangRelease(player)
```

---

## Examples

Check for a single release:

```js
var fire = stats.getFireRelease(event.player);
if (fire > 0) {
    event.player.message("You know Fire Release!");
}
```

Check for a combination:

```js
var fire = stats.getFireRelease(event.player);
var water = stats.getWaterRelease(event.player);
if (fire > 0 && water > 0) {
    event.player.message("You can learn Boil Release!");
}
```
