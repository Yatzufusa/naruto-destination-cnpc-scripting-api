# Abilities

## Sage

### getSageMode
```js
boolean stats.getSageMode(player)
```
Whether the player has Sage Mode unlocked. Changing something

---

### getSageVersion
```js
int stats.getSageVersion(player)
```
Which Sage Mode variant the player has.

---

## Susanoo

### getSusanoSize
```js
int stats.getSusanoSize(player)
```
Unlocked Susanoo size/stage.

---

## Curse Seal

### getCurseSeal
```js
int stats.getCurseSeal(player)
```
Curse seal type. `0` = none.

---

### getCurseSize
```js
int stats.getCurseSize(player)
```
Curse seal stage.

---

## Six Paths

### getTruthseekingOrbs
```js
boolean stats.getTruthseekingOrbs(player)
```
Whether the player has Truth-Seeking Orbs.

---

## Eight Gates

### getEightGatesUnlocked
```js
int stats.getEightGatesUnlocked(player)
```
How many gates the player has unlocked (0-8).

---

## Byakugou

### getByakugouUnlocked
```js
int stats.getByakugouUnlocked(player)
```
Byakugou unlock level.

---

## Karma Seal

### getKarmaSealSize
```js
int stats.getKarmaSealSize(player)
```
Karma Seal stage.

---

## Otsutsuki

### getOtsutsukiDNA
```js
int stats.getOtsutsukiDNA(player)
```
Otsutsuki DNA type.

---

### getOtsutsukiUnlockedSize
```js
int stats.getOtsutsukiUnlockedSize(player)
```
Unlocked Otsutsuki stage.

---

## Kenjutsu

### getKenjutsuSkills
```js
int stats.getKenjutsuSkills(player)
```
Unlocked kenjutsu skills (bitmask).

---

## Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;

    if (stats.getSageMode(player)) {
        player.message("A Sage... impressive.");
    }

    var gates = stats.getEightGatesUnlocked(player);
    if (gates >= 6) {
        player.message("You've opened " + gates + " gates. Dangerous.");
    }

    if (stats.getTruthseekingOrbs(player)) {
        player.message("The power of Six Paths flows through you.");
    }
}
```
