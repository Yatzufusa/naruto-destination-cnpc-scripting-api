# Clan & Affiliation

## Clan

### getClan
```js
int stats.getClan(player)
```
Clan ID as an integer.

---

### getClanName
```js
String stats.getClanName(player)
```
Clan name, e.g. `"Uchiha"`, `"Uzumaki"`, `"Hyuga"`.

---

## Rank

### getRank
```js
String stats.getRank(player)
```
Rank as a string ID, e.g. `"Genin"`, `"Chunin"`, `"Jonin"`, `"Kage"`, `"Akatsuki"`.

Some ranks with multiple words use camelCase: `"AcademyStudent"`, `"TokubetsuJonin"`, `"AnbuCaptain"`, `"Missing-Nin"`.

See the full list of rank IDs in the table below.

??? note "All Rank IDs"
    | Rank ID | Display Name |
    |---|---|
    | `Villager` | Villager |
    | `AcademyStudent` | Academy Student |
    | `Genin` | Genin |
    | `Chunin` | Chunin |
    | `TokubetsuJonin` | Tokubetsu Jonin |
    | `Jonin` | Jonin |
    | `Missing-Nin` | Missing-Nin |
    | `ExplosionCorps` | Explosion Corps |
    | `Taka` | Taka |
    | `Hebi` | Hebi |
    | `oftheBloodyMist` | of the Bloody Mist |
    | `Samurai` | Samurai |
    | `Anbu` | Anbu |
    | `MedicalTeam` | Medical Team |
    | `IntelTeam` | Intel Team |
    | `AnbuCaptain` | Anbu Captain |
    | `MedicalCaptain` | Medical Captain |
    | `IntelCaptain` | Intel Captain |
    | `Akatsuki` | Akatsuki |
    | `KinkakuForce` | Kinkaku Force |
    | `12GuardianNinja` | 12 Guardian Ninja |
    | `PuppetBrigade` | Puppet Brigade |
    | `7NinjaSwordsmen` | 7 Ninja Swordsmen o/t Mist |
    | `Kage` | Kage |
    | `AkatsukiLeader` | Akatsuki Leader |
    | `Sannin` | Sannin |
    | `D-Rank` | D-Rank |
    | `C-Rank` | C-Rank |
    | `B-Rank` | B-Rank |
    | `A-Rank` | A-Rank |
    | `S-Rank` | S-Rank |
    | `TailedBeast` | Tailed Beast |
    | `Advisor` | Advisor |
    | `ShadowKage` | Shadow Kage |
    | `WhiteFang` | White Fang |
    | `oftheSharingan` | of the Sharingan |
    | `YellowFlash` | Yellow Flash |
    | `GreenBeast` | Green Beast |
    | `Hokage` | Hokage |
    | `Kazekage` | Kazekage |
    | `Mizukage` | Mizukage |
    | `Tsuchikage` | Tsuchikage |
    | `Raikage` | Raikage |
    | `Rogue` | Rogue |
    | `SeniorAkatsuki` | Senior Akatsuki |

---

## Affiliation

### getAffiliation
```js
int stats.getAffiliation(player)
```
Village affiliation ID.

---

### getAffiliationName
```js
String stats.getAffiliationName(player)
```
Village name as a string.

---

## Land

### getLand
```js
int stats.getLand(player)
```
Land ID.

---

## Example

```js
var stats = Java.type("narutodestination.Mathioks.CNPC.CustomNPCStatsHandler");

function interact(event) {
    var player = event.player;
    var clan = stats.getClanName(player);
    var rank = stats.getRank(player);
    var village = stats.getAffiliationName(player);

    player.message("You are a " + rank + " of the " + clan + " clan");
    player.message("Village: " + village);
}
```
