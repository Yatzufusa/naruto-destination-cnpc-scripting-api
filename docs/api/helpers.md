# Helpers

Methods that return arrays of everything a player has unlocked.

## getKnownReleases
```js
String[] stats.getKnownReleases(player)
```
All nature release names the player has.

---

## getKnownClans
```js
String[] stats.getKnownClans(player)
```
All clan names the player belongs to.

---

## getKnownBijuu
```js
String[] stats.getKnownBijuu(player)
```
Tailed beast names the player knows about.

---

## Examples

```js
var releases = stats.getKnownReleases(event.player);
event.player.message("You know " + releases.length + " releases:");
for (var i = 0; i < releases.length; i++) {
    event.player.message("- " + releases[i]);
}
```

```js
var clans = stats.getKnownClans(event.player);
event.player.message("Clan Count: " + clans.length);
for (var i = 0; i < clans.length; i++) {
    event.player.message("- " + clans[i]);
}
```
