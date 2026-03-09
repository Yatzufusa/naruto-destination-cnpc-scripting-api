# Clan Checks

All return `boolean` — `true` if the player has the clan, `false` if not.

| Method | Clan |
|---|---|
| `hasUchihaClan(player)` | Uchiha |
| `hasUzumakiClan(player)` | Uzumaki |
| `hasHyugaClan(player)` | Hyuga |
| `hasSenjuClan(player)` | Senju |
| `hasAburameClan(player)` | Aburame |
| `hasHatakeClan(player)` | Hatake |
| `hasHozukiClan(player)` | Hozuki |
| `hasIburiClan(player)` | Iburi |
| `hasInuzukaClan(player)` | Inuzuka |
| `hasJugoClan(player)` | Jugo |
| `hasKaguyaClan(player)` | Kaguya |
| `hasKuramaClan(player)` | Kurama |
| `hasTsuchigumoClan(player)` | Tsuchigumo |
| `hasNaraClan(player)` | Nara |
| `hasSarutobiClan(player)` | Sarutobi |
| `hasFumaClan(player)` | Fuma |
| `hasYukiClan(player)` | Yuki |
| `hasYamanakaClan(player)` | Yamanaka |
| `hasLeeClan(player)` | Lee |
| `hasChinoikeClan(player)` | Chinoike |
| `hasNamikazeClan(player)` | Namikaze |
| `hasShiroganeClan(player)` | Shirogane |

For getting all clans as an array, use [`getKnownClans()`](helpers.md) instead.

## Examples

```js
if (stats.hasUchihaClan(event.player)) {
    event.player.message("Welcome, Uchiha.");
}
```

```js
var clanCount = 0;
if (stats.hasUchihaClan(event.player)) clanCount++;
if (stats.hasSenjuClan(event.player)) clanCount++;
if (stats.hasUzumakiClan(event.player)) clanCount++;
event.player.message("You are part of " + clanCount + " clans!");
```
