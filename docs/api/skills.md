# Skills

All skill methods return `int`. Values go from 0 upwards.

## getNinjutsu
```js
int stats.getNinjutsu(player)
```

---

## getTaijutsu
```js
int stats.getTaijutsu(player)
```

---

## getGenjutsu
```js
int stats.getGenjutsu(player)
```

---

## getKenjutsu
```js
int stats.getKenjutsu(player)
```

---

## getShurikenJutsu
```js
int stats.getShurikenJutsu(player)
```

---

## getMedical
```js
int stats.getMedical(player)
```

---

## getSummoning
```js
int stats.getSummoning(player)
```

---

## getKinjutsu
```js
int stats.getKinjutsu(player)
```

---

## getSenjutsu
```js
int stats.getSenjutsu(player)
```

---

## getSpeed
```js
int stats.getSpeed(player)
```

---

## Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;
    var nin = stats.getNinjutsu(player);
    var tai = stats.getTaijutsu(player);
    var totalPower = nin + tai;

    player.message("Ninjutsu: " + nin + " | Taijutsu: " + tai);
    player.message("Combined power: " + totalPower);
}
```
