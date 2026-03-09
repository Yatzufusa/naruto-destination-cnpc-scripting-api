# Kekkei Genkai

## Combined Releases

All return `int` — `0` means not unlocked, `1` means unlocked.

### getWoodRelease
```js
int stats.getWoodRelease(player)
```

### getLavaRelease
```js
int stats.getLavaRelease(player)
```

### getScorchRelease
```js
int stats.getScorchRelease(player)
```

### getBoilRelease
```js
int stats.getBoilRelease(player)
```

### getMagnetRelease
```js
int stats.getMagnetRelease(player)
```

### getStormRelease
```js
int stats.getStormRelease(player)
```

### getIceRelease
```js
int stats.getIceRelease(player)
```

### getExplosionRelease
```js
int stats.getExplosionRelease(player)
```

### getSteelRelease
```js
int stats.getSteelRelease(player)
```

### getCrystalRelease
```js
int stats.getCrystalRelease(player)
```

### getDustRelease
```js
int stats.getDustRelease(player)
```

### getShikotsumyaku
```js
int stats.getShikotsumyaku(player)
```
Bone Release (Kaguya clan).

---

## Dojutsu

### getSharinganSize
```js
int stats.getSharinganSize(player)
```

| Value | Stage |
|---|---|
| `0` | No Sharingan |
| `1` | 1 Tomoe |
| `2` | 2 Tomoe |
| `3` | 3 Tomoe |
| `4` | Mangekyou Sharingan |
| `5` | Eternal Mangekyou Sharingan |
| `6` | Rinnegan |

---

### getMangekyouSharingan
```js
String stats.getMangekyouSharingan(player)
```
The MS pattern name. Empty if the player doesn't have one.

---

### getByakugan
```js
int stats.getByakugan(player)
```
`0` = no Byakugan.

---

### getTenseigan
```js
int stats.getTenseigan(player)
```
`0` = no Tenseigan.

---

### getKetsuryugan
```js
int stats.getKetsuryugan(player)
```
`0` = no Ketsuryugan.

---

### getJougan
```js
int stats.getJougan(player)
```
`0` = no Jougan.

---

## Examples

```js
var sharingan = stats.getSharinganSize(event.player);
if (sharingan > 0) {
    event.player.message("You have the Sharingan!");
}
if (sharingan >= 4) {
    event.player.message("Your Mangekyou has awakened...");
}
```

```js
if (stats.getWoodRelease(event.player) > 0) {
    event.player.message("You have Wood Release!");
}
```
