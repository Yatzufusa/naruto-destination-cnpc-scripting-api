# General Stats

## getLevel
```js
int stats.getLevel(player)
```
Player's current level.

---

## getSkillPoints
```js
int stats.getSkillPoints(player)
```
Unspent skill points.

---

## getAllSkillPoints
```js
int stats.getAllSkillPoints(player)
```
Total skill points ever earned (spent + unspent), excluding bonus points from Sage Soup.

---

## getAllAssignedSkillPoints
```js
int stats.getAllAssignedSkillPoints(player)
```
Total skill points the player has spent across all skills.

---

## getJutsuPoints
```js
int stats.getJutsuPoints(player)
```
Unspent jutsu points.

---

## getResetPoints
```js
int stats.getResetPoints(player)
```
Available reset points.

---

## getIntelligence
```js
int stats.getIntelligence(player)
```
Intelligence stat value.

---

## getChakraControl
```js
boolean stats.getChakraControl(player)
```
Whether the player has chakra control unlocked.

---

## getSageSoupCounter
```js
int stats.getSageSoupCounter(player)
```
How many times the player has used Sage Soup.

---

## Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;
    var sp = stats.getSkillPoints(player);
    var lvl = stats.getLevel(player);
    player.message("Level " + lvl + " | SP: " + sp);
}
```
