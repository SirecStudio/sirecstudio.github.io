# Configuration Helps

## SS-Weapons Setup & Configuration Guide

SS-Weapons is a RedM weapon catalogue, ammo, blueprint gunsmith, weapon condition, cleaning, repair, HUD and preview system.

This guide is written for server owners who want to install, configure and test the script safely.

***

## Features Overview

* Vintage catalogue store with configurable weapon and ammo lists per location.
* Ammo boxes that add bullets to the player's ammo belt.
* Blueprint gunsmith editor: every editable part linked to the real weapon on the bench, options drawer, live preview, rotate / zoom / reset.
* Automatic centering and framing of the preview for every weapon; per-weapon presets tuned in game.
* Per-weapon part lists (only what the game accepts), bow colours, blade materials and engravings.
* Gunsmith templates for saving and reusing setups.
* Custom weapon serial and custom weapon name, per store.
* Persistent dirt, soot, degradation, damage and permanent wear; cleaning through the native inspection flow; repair kit.
* One player per bench; nearby players can watch the preview.
* Optional weapon HUD, poison / tranquilizer effects.
* vorp\_inventory v1 and v2, server-side validation of every purchase and edit.
* 8 languages.

***

## Dependencies

### Required

* `SS-Core`
* `ghmattimysql`
* `vorp_inventory` (v1 or v2, detected automatically)

### Used By Default

* `@SS-Core/dataview.lua`
* `vorp:NotifyLeft` in the default `NOTIFY` function (`config.lua`).

### Optional Integrations

* `SS-Notify`, if you switch the `NOTIFY` function to the commented example.
* `SS-PlayerShops`, if you use the external player shop flow supported by the client.

***

## Installation

### 1. Add The Resource

```
resources/[scripts]/SS-Weapons
```

Keep the folder name exactly `SS-Weapons`: the script checks it and the NUI posts to it.

### 2. Database

Tables are created and upgraded automatically at start:

```
ss_weapons
ss_weaponstemp
```

The script also reads and updates your existing weapon `loadout` table.

### 3. Start Order

```cfg
ensure ghmattimysql
ensure vorp_inventory
ensure SS-Core
ensure SS-Weapons
```

### 4. vorp\_inventory v2

v2 ships its own weapon degradation and component loading. To let SS-Weapons own them, set in the inventory config:

```lua
CONFIG.USE_WEAPON_DEGRADATION = false
CONFIG.USE_WEAPON_COMPONENTS = false
```

then set `InventoryDegradationHandled = true` in SS-Weapons. Leave `InventoryVersion = "auto"`.

### 5. Restart

Restart the server and test one store, one bench, one ammo box, one cleaning item and one repair item.

***

## Main Files

* `config.lua`: Main configuration.
* `cfg/weapons.lua` / `cfg/ammo.lua`: Catalogs.
* `cfg/anchors.lua`: Callout line positions per weapon type.
* `cfg/presets.json`: Per-weapon camera and callout presets (saved by the server).
* `l/l.lua`: Notification translations.
* `config.js`: UI language and UI options.
* `UI/`: Catalogue and gunsmith UI.

***

## Languages

Set the same language in two files:

```lua
-- config.lua
Language = "RO"
```

```js
// config.js
var Config = { Language: "RO" };
```

Included: `EN`, `IT`, `ES`, `FR`, `DE`, `PT`, `RU`, `RO`.

***

## Stores

Each store can enable the catalogue, the bench, or both:

```lua
EnableStore = true
EnableGunsmith = true
```

What each store sells:

```lua
WichWeapons = false   -- false = all, {} = none, {"WEAPON_..."} = only listed
WichAmmo = false
```

Custom serial / name per store:

```lua
Serial = true          -- true = paid option, false = hidden
CustomLabel = true     -- true = paid option, false = hidden, "Text" = forced free name
```

***

## Add A New Store

Copy an existing entry and change name, positions, cameras, blips and jobs:

```lua
[5] = {
    Name = "Annesburg",

    EnableStore = true,
    StoreBlip = 202506373,
    CatalogWeapon = {2946.54, 1319.93, 44.82, 246.31},
    CamStore = {2947.55, 1319.71, 45.62, -90.0, 110.0, 0.0, 50.0},
    WichWeapons = false,
    WichAmmo = false,
    Serial = true,
    CustomLabel = true,

    EnableGunsmith = true,
    GunSmithBlip = 202506373,
    ModifyWeapons = {2949.89, 1314.15, 44.91},
    ModifyPos = {2949.89, 1314.15, 44.91, 90.0, 163.0, 178.0},
    CamGunSmith = {2950.21, 1314.14, 45.41, -90.0, 200.0, 0.0, 80.0},
    Jobs = {"Armurier"},
},
```

Tips for the bench: `ModifyPos` is where the weapon lies, `CamGunSmith` looks straight down at it (pitch `-90.0`). Thanks to auto centering and auto fit you only need the camera roughly above the bench; the script centres and frames the weapon itself.

***

## Weapon Catalog

`cfg/weapons.lua` controls per weapon: name / hash, label and title, description and extra text, category, price, gold value, buy jobs and grades, modify jobs and grades, type.

```lua
BuyJobs = {"police"}        -- only these jobs can buy
BuyJobsGrade = {2}
ModifyJobs = {"Armurier"}   -- only these jobs can customize it at a bench
```

Empty tables mean everyone.

***

## Ammo Catalog

`cfg/ammo.lua` fields: `Item` (inventory item), `Label`, `Category`, `Price` per box, `Type` (ammo type added to the belt), `MaxAmmo` (belt limit), `Amount` (bullets per box).

***

## Buying Flow

1. Player opens a store: the catalogue shows weapons and ammo by category.
2. Player picks an item, optionally a custom serial / name or an ammo quantity.
3. One server call rebuilds the price from the config, checks money and carry space, charges and gives the item.
4. Ammo boxes are used later to add bullets to the belt.

***

## Gunsmith Flow

1. Player equips a supported weapon and walks to a bench (job checked on client and server; the bench must be free).
2. The weapon is put away, the preview spawns on the bench and the camera glides above it. The preview is centred and framed automatically.
3. Cards for every editable part appear with a line to the part on the weapon. Click a card to open the options drawer; pick tiles, watch the preview update, see the price per change.
4. Templates can be saved / applied / deleted; the hammer button repairs the weapon.
5. Confirm & pay: the server prices the difference from what is stored, charges and saves the components. Re-equip the weapon to carry the new look.

***

## Weapon Presets (camera + callouts per weapon)

If a weapon sits too small, off centre, or a callout points beside its part:

1. Set `Dev = true`, equip the weapon and open a bench. The **Weapon preset** panel appears bottom-left.
2. **Camera**: pan left / right, pan up / down, distance, turn and FOV move the camera; **Weapon turn** rotates the weapon on the bench; **Reset cam** drops the changes.
3. **Anchor**: pick a part and nudge it Right / Forward / Up until the ring sits on the right spot. Only moved parts are stored.
4. **Save preset** writes camera + moved anchors for this weapon to `cfg/presets.json` and sends them to all clients. **Delete preset** removes them. **Print table** prints values and model diagnostics to F8.
5. Ship `cfg/presets.json` with the resource and set `Dev = false` again.

***

## Gunsmith Prices

Prices per part category and edit type live in `Config.GunSmith`; payment type in `WeaponEditPayment.Type` (`gold` or `money`). See Configuration File for the full table.

***

## Gunsmith Templates

Players save, apply and delete component setups. Stored in `ss_weaponstemp` by identifier, character ID, weapon and template name.

***

## Weapon Cleaning

```lua
CleanWeaponItem = "leather"
RemoveAfterClean = true
CleanWeaponTime = 10000
MinCleanWeaponTime = 2500
InspectWeaponCommand = "w_inspect"
```

Use the clean item (or `/w_inspect`) with the weapon in hand: the native inspection opens, the clean prompt removes dirt / soot / degradation and adds a little permanent wear. `/w_inspectstatus` prints why inspection is blocked, `/w_inspectreset` frees a stuck interaction.

***

## Weapon Repair

```lua
WeaponRepair = {
    Enabled = true,
    Item = "weapon_repair_kit",
    RemoveItem = true,
    RepairAmount = 0.10,
    MinRustRequired = 0.01,
}
```

Repair is started from the editor and lowers the permanent wear stored on the server.

***

## Weapon Wear

`ss_weapons` stores per serial: weapon name, last loadout ID, dirt, soot, condition, damage and permanent wear. Wear sent by clients can only grow; only cleaning and repair lower it. With `UseDegradation = true` a weapon at 100% permanent wear cannot fire.

***

## Weapon HUD

```lua
WeaponHud = { Enabled = false, Position = "top-right", UpdateInterval = 150, HideWhenUiOpen = true }
```

Icons: `UI/img/weapons` (lower-case weapon name) and `UI/img/ammo_types`.

***

## Preview Sync & Bench Lock

```lua
PreviewSync = { Enabled = true, Radius = 8.0, MaxSpectators = 6, CheckInterval = 2000 }
```

Nearby players see the preview while someone edits. A bench in use is locked: others get "This workbench is being used by someone else" until the player leaves, pays or disconnects.

***

## Poison & Tranquilizer

```lua
ActivePoison = false
ActiveTranq = false
```

Disabled by default; enable only if your server uses poison arrows or tranquilizer gameplay.

***

## Dev Commands & Tools

With `Dev = true`: `/dirtyweapon`, `/wstatus`, `/wdirt`, `/wsoot`, `/wdegradation`, `/wdamage`, `/wthreshold`, `/wwear`, `/wresetwear`, the Weapon preset panel, and `[SS-Weapons][Equip]` / `[SS-Weapons][Anchors]` prints in F8.

Always available: `/w_inspect`, `/w_inspectstatus`, `/w_inspectreset`.

***

## Troubleshooting

### Store Prompt Does Not Appear

* `EnableStore = true`, `CatalogWeapon` coordinates, `PressKey`, folder named `SS-Weapons`.

### Bench Prompt Does Not Appear

* `EnableGunsmith = true`, `ModifyWeapons` coordinates, player job in `Jobs`.

### "Re-equip the weapon"

* Equip the weapon once from the inventory so the script receives it. Weapons received at character select are dressed when drawn. On v2, draw the weapon you want to edit before pressing the prompt.

### "This workbench is being used by someone else"

* Another player has the bench open. Locks are released on leave / pay / disconnect and expire on their own.

### Wrong Weapon On The Bench / Mods Not Applied (vorp\_inventory v2)

* Make sure the server runs the current `c/c.lua` and `s/s.lua`, `InventoryVersion = "auto"`, and v2 has `USE_WEAPON_DEGRADATION = false` and `USE_WEAPON_COMPONENTS = false`.

### Callout Lines In The Wrong Place

* Tune the weapon in the Dev preset panel and Save preset; check `SideSign` / `MuzzleAtPositiveEnd` in `cfg/anchors.lua` if a whole weapon type is mirrored.

### Player Cannot Buy

* Money, carry limits from `SS-Core`, item exists in `cfg/weapons.lua` / `cfg/ammo.lua`, player stands at the counter, custom name within `MinLabel` / `MaxLabel`.

### Ammo Item Does Not Add Bullets

* Ammo item name matches the inventory item, `Type` is correct, belt not full, `MaxAmmo` / `Amount` correct.

### Weapon HUD Image Is Missing

* Image exists in `UI/img/weapons` with the lower-case weapon name; ammo icon exists in `UI/img/ammo_types`.

### Cleaning Does Not Work

* Player has `CleanWeaponItem`, weapon in hand, run `/w_inspectstatus` for the exact blocker.

### Repair Does Not Work

* `WeaponRepair.Enabled = true`, player has the repair item, weapon has at least `MinRustRequired` permanent wear.

***

## Recommended Live Checklist

* `ghmattimysql`, `vorp_inventory`, `SS-Core` start before `SS-Weapons`.
* Resource folder named `SS-Weapons`.
* `Dev = false`.
* Same language in `config.lua` and `config.js`.
* `cfg/presets.json` shipped.
* Stores, benches, buying, ammo, edit / pay, templates, cleaning, repair, HUD and preview sync tested.

***

## Editing Rules For Beginners

* Strings use quotes: `"text"`. Table entries end with a comma.
* `true` enables a feature; `false` disables it or means all / everyone depending on the field.
* Numbers do not use quotes. Coordinates use `{x, y, z}` or `{x, y, z, heading}`.
* Do not rename the resource folder.

Bad: `Dev = "false"` — Good: `Dev = false`
