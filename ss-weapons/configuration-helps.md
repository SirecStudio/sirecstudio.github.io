# Configuration Helps

## SS-Weapons Setup & Configuration Guide

SS-Weapons is a RedM weapon store, ammo, gunsmith, customization, weapon condition, cleaning, repair, HUD, and preview system.

This guide is written for server owners who want to install, configure, and test the script safely.

***

## Features Overview

SS-Weapons includes:

* Weapon stores with configurable weapon and ammo catalogs.
* Ammo boxes that add bullets to the player's ammo belt.
* Gunsmith benches with job restrictions.
* Weapon component customization.
* Gunsmith templates for saving and reusing component setups.
* Custom weapon serial and custom weapon label support.
* Persistent weapon dirt, soot, condition, damage, and rust/wear.
* Weapon cleaning through the native inspection flow.
* Weapon repair with configurable repair item.
* Optional weapon HUD with weapon image and ammo count.
* Gunsmith preview sync for nearby players.
* Optional poison and tranquilizer effects.
* Multi-language support.

***

## Dependencies

### Required

* `SS-Core`
* `ghmattimysql`
* `vorp_inventory`

### Used By Default

* `@SS-Core/dataview.lua`
* `vorp:NotifyLeft` in the default `NOTIFY` function.
* RedM/RDR3 weapon native functions.

### Optional Integrations

* `SS-Notify`, if you switch the `NOTIFY` function to the included commented example.
* `SS-PlayerShops`, if you use the external player shop open/buy flow already supported by the client.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-Weapons
```

Keep the resource folder name exactly:

```text
SS-Weapons
```

The script checks the resource name, and the NUI expects `SS-Weapons`.

### 2. Database

SS-Weapons creates and upgrades its own extra tables automatically:

```text
ss_weapons
ss_weaponstemp
```

The script also reads and updates your existing weapon `loadout` table.

Make sure your server already has the standard weapon/loadout setup used by `SS-Core` and your inventory.

### 3. Start Order

Recommended:

```cfg
ensure ghmattimysql
ensure vorp_inventory
ensure SS-Core
ensure SS-Weapons
```

If you use `SS-Notify`, start it before `SS-Weapons`.

### 4. Restart The Server

After checking dependencies, start order, and config, restart the server and test one store, one gunsmith bench, one ammo box, one cleaning item, and one repair item.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main configuration.
* `cfg/weapons.lua`: Weapon catalog.
* `cfg/ammo.lua`: Ammo catalog.
* `l/l.lua`: Lua translations.
* `config.js`: UI translations and book UI settings.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Weapon store and gunsmith UI.

***

## Languages

Languages are configured in:

```text
config.lua
```

Example:

```lua
Language = "RO"
```

Included languages:

* `EN`
* `IT`
* `ES`
* `FR`
* `DE`
* `PT`
* `RU`
* `RO`

Lua translations are in:

```text
l/l.lua
```

UI translations are in:

```text
config.js
```

***

## First Configuration

Open:

```text
config.lua
```

Start with:

```lua
Dev = false
Language = "EN"
PressKey = 0xD9D0E1C0
WaitingAnime = true
```

* `Dev`: Keep `false` on live servers.
* `Language`: Main script language.
* `PressKey`: Key used to open store and gunsmith prompts.
* `WaitingAnime`: Keeps the player in an idle animation while UI is open.

***

## Stores

Stores are configured in:

```text
config.lua
```

Each store can enable a buy catalog, a gunsmith bench, or both.

```lua
EnableStore = true
EnableGunsmith = true
```

Use these fields to control what each store sells:

```lua
WichWeapons = false
WichAmmo = false
```

Meaning:

* `false`: Sell all configured weapons/ammo.
* `{}`: Sell nothing from that type.
* `{ "WEAPON_REVOLVER_CATTLEMAN" }`: Sell only listed entries.

***

## Add A New Store

Copy an existing store entry and change the name, positions, cameras, blips, and jobs.

```lua
[5] = {
    Cover = "coverbook",
    Name = "Annesburg",

    EnableStore = true,
    StoreBlip = 202506373,
    CatalogWeapon = {2946.54, 1319.93, 44.82, 246.31},
    CamStore = {2947.55, 1319.71, 45.62, -90.0, 110.0, 0.0, 50.0},
    WichWeapons = false,
    WichAmmo = false,

    EnableGunsmith = true,
    GunSmithBlip = 202506373,
    ModifyWeapons = {2949.89, 1314.15, 44.91},
    ModifyPos = {2949.89, 1314.15, 44.91, 90.0, 163.0, 178.0},
    CamGunSmith = {2950.21, 1314.14, 45.41, -90.0, 200.0, 0.0, 80.0},
    Jobs = {"Armurier"},
},
```

After adding a store, restart the resource and test both prompt positions.

***

## Weapon Catalog

Weapons are configured in:

```text
cfg/weapons.lua
```

Each weapon can control:

* Weapon hash/name.
* Label and title.
* Description and extra text.
* Category.
* Money price.
* Gold value.
* Buy job restrictions.
* Modify job restrictions.
* Weapon type.

If a weapon should only be sold to specific jobs, fill:

```lua
BuyJobs = {"police"}
BuyJobsGrade = {2}
```

If everyone can buy it, leave:

```lua
BuyJobs = {}
BuyJobsGrade = {}
```

***

## Ammo Catalog

Ammo is configured in:

```text
cfg/ammo.lua
```

Important fields:

* `Item`: Inventory item name.
* `Label`: UI label.
* `Category`: UI category.
* `Price`: Price per ammo box.
* `Type`: Ammo type added to the belt.
* `MaxAmmo`: Maximum belt amount.
* `Amount`: Bullets added by one box.

Example:

```lua
["ammorevolvernormal"] = {
    Item = "ammorevolvernormal",
    Label = "Revolver Normal Ammo",
    Price = 50,
    Type = "AMMO_REVOLVER",
    MaxAmmo = 200,
    Amount = 100,
}
```

***

## Buying Flow

Weapon buying works like this:

1. Player opens a configured store.
2. UI displays weapons and ammo by category.
3. Player chooses custom serial or label if the store allows it.
4. Client asks the server if the player has money and carry space.
5. Server gives the weapon or ammo item.
6. Ammo boxes can later be used to add bullets to the ammo belt.

***

## Gunsmith Flow

Gunsmith editing works like this:

1. Player equips a supported weapon.
2. Player goes to a gunsmith bench.
3. Script checks job access.
4. Preview weapon spawns on the bench.
5. UI opens component notes and selections.
6. Player changes components and sees the price update.
7. Server syncs preview changes to nearby spectators if enabled.
8. Player pays and saves components to the weapon loadout.

***

## Gunsmith Prices

Gunsmith prices are configured in:

```lua
GunSmith = {
    ["GRIP"] = {
        ["COMP"] = 45,
        ["MATERIAL"] = 20,
        ["ENGRAVE"] = 20,
        ["ENGRAVEM"] = 20,
        ["TINT"] = 20,
    },
}
```

Payment type:

```lua
WeaponEditPayment = {
    Type = "gold",
}
```

Use `gold` or `money`.

***

## Gunsmith Templates

Templates let players save, apply, and delete weapon component setups.

Stored table:

```text
ss_weaponstemp
```

Templates are saved by:

* Identifier.
* Character ID.
* Weapon.
* Template name.

***

## Weapon Cleaning

Cleaning settings:

```lua
CleanWeaponItem = "leather"
RemoveAfterClean = true
CleanWeaponTime = 10000
MinCleanWeaponTime = 2500
InspectWeaponCommand = "w_inspect"
```

Cleaning uses the native weapon inspection flow and can reduce dirt, soot, and runtime degradation.

***

## Weapon Repair

Repair settings:

```lua
WeaponRepair = {
    Enabled = true,
    Item = "weapon_repair_kit",
    RemoveItem = true,
    RepairAmount = 0.10,
    MinRustRequired = 0.01,
}
```

Repair reduces permanent rust/damage stored by the script.

***

## Weapon Wear

Stored table:

```text
ss_weapons
```

The script stores:

* Serial number.
* Weapon name.
* Last loadout ID.
* Dirt level.
* Soot level.
* Condition level.
* Damage level.
* Rust/permanent wear level.

When `UseDegradation = true`, permanent wear can eventually make a weapon unusable.

***

## Weapon HUD

Weapon HUD settings:

```lua
WeaponHud = {
    Enabled = false,
    Position = "top-right",
    UpdateInterval = 150,
    HideWhenUiOpen = true,
}
```

Weapon icons are loaded from:

```text
UI/img/weapons
```

Ammo icons are loaded from:

```text
UI/img/ammo_types
```

***

## Preview Sync

Preview sync settings:

```lua
PreviewSync = {
    Enabled = true,
    Radius = 8.0,
    MaxSpectators = 6,
    CheckInterval = 2000,
}
```

When enabled, nearby players can see the gunsmith preview weapon while someone edits it.

***

## Poison & Tranquilizer

These systems are disabled by default:

```lua
ActivePoison = false
ActiveTranq = false
```

Enable them only if your server intentionally uses poison arrow or tranquilizer gameplay.

***

## Dev Commands

These commands are only for testing and require:

```lua
Dev = true
```

Commands:

* `/dirtyweapon`
* `/wstatus`
* `/wdirt`
* `/wsoot`
* `/wdegradation`
* `/wdamage`
* `/wthreshold`
* `/wwear`
* `/wresetwear`

Normal inspect command:

```text
/w_inspect
```

***

## Troubleshooting

### Store Prompt Does Not Appear

Check:

* `EnableStore = true`.
* `CatalogWeapon` coordinates.
* `PressKey`.
* Resource folder name is exactly `SS-Weapons`.

### Gunsmith Prompt Does Not Appear

Check:

* `EnableGunsmith = true`.
* `ModifyWeapons` coordinates.
* Player job is allowed in `Jobs`.

### Player Cannot Edit Weapon

Check:

* Weapon is equipped.
* Weapon is supported by component data.
* Player re-equipped the weapon after receiving it.
* Job restrictions allow the player.

### Player Cannot Buy

Check:

* Player has enough money.
* Carry limits from `SS-Core`.
* Weapon exists in `cfg/weapons.lua`.
* Ammo exists in `cfg/ammo.lua`.

### Ammo Item Does Not Add Bullets

Check:

* Ammo item name matches the inventory item.
* `Type` is correct.
* Belt is not already full.
* `MaxAmmo` and `Amount` are correct.

### Weapon HUD Image Is Missing

Check:

* Weapon image exists in `UI/img/weapons`.
* File name matches the lower-case weapon name.
* Ammo icon exists in `UI/img/ammo_types`.

### Cleaning Does Not Work

Check:

* Player has `CleanWeaponItem`.
* Weapon is equipped.
* Native inspection starts.
* `RemoveAfterClean` is configured correctly.

### Repair Does Not Work

Check:

* `WeaponRepair.Enabled = true`.
* Player has the repair item.
* Weapon has at least `MinRustRequired` permanent damage.

***

## Recommended Live Checklist

Before going live, confirm:

* `ghmattimysql` starts before `SS-Weapons`.
* `vorp_inventory` starts before `SS-Weapons`.
* `SS-Core` starts before `SS-Weapons`.
* Resource folder is named `SS-Weapons`.
* `Dev = false`.
* Stores open correctly.
* Gunsmith benches open correctly.
* Weapon buying works.
* Ammo buying and ammo item usage work.
* Gunsmith edit/save works.
* Template save/apply/delete works.
* Weapon cleaning works.
* Weapon repair works.
* Weapon HUD works if enabled.
* Preview sync works if enabled.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature.
* `false` disables a feature or means all/everyone depending on the field.
* Numbers do not use quotes.
* Coordinates use `{x, y, z}` or `{x, y, z, heading}` style.
* Do not rename the resource folder.

Bad:

```lua
Dev = "false"
```

Good:

```lua
Dev = false
```
