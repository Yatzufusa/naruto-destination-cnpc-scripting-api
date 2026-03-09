# Bijuu

## getBijuuKind
```js
int stats.getBijuuKind(player)
```
Which tailed beast the player is a jinchuriki of. `0` = not a jinchuriki.

---

## getBijuuUnlock
```js
double stats.getBijuuUnlock(player)
```
Bijuu unlock progress (decimal).

---

## getBijuuScale
```js
int stats.getBijuuScale(player)
```
Bijuu transformation scale.

---

## getKnownBijuu
```js
String[] stats.getKnownBijuu(player)
```
Array of tailed beast names the player knows about.

---

## Examples

```js
var bijuuKind = stats.getBijuuKind(event.player);
if (bijuuKind > 0) {
    event.player.message("You carry a Tailed Beast within you.");
} else {
    event.player.message("You are not a jinchuriki.");
}
```

```js
var bijuu = stats.getKnownBijuu(event.player);
event.player.message("You know about " + bijuu.length + " Tailed Beasts:");
for (var i = 0; i < bijuu.length; i++) {
    event.player.message("- " + bijuu[i]);
}
```
