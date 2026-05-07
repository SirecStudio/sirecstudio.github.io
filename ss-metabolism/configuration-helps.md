# Configuration Helps

## SS-Metabolism Setup & Configuration Guide

SS-Metabolism is a RedM metabolism HUD script with a custom NUI interface. It manages hunger, thirst, stress, dirtiness, reputation, health and stamina cores, horse stats, temperature, housing indicators, voice status, clock display, HUD editing, and usable item effects.

This guide is written for server owners who want to install, configure, and test the script safely, even without deep Lua knowledge.

***

## Features Overview

SS-Metabolism includes:

* Custom Red Dead Redemption style HUD.
* Hunger, thirst, stress, dirtiness, and reputation tracking.
* Player health and stamina inner/outer cores.
* Horse health, stamina, hunger, and thirst HUD support.
* Temperature and outside degrees display.
* Housing icon support through exports.
* Voice/microphone status and pma-voice range display.
* Analog or digital in-game clock.
* HUD editor through `/sethud`.
* HUD toggle through `/shud`.
* Saved HUD positions, scale, and hidden icons.
* Usable food, drink, alcohol, drug, and medicine item support through `SS-Core`.

***

## Dependencies

### Required

* `SS-Core`
* `oxmysql`

### Used By Default

* RedM NUI
* `vorp:TipBottom`, used for notifications.

### Optional / External Behavior

* `pma-voice` for microphone talking status and voice range.
* Housing scripts can call the housing exports.
* Stable or horse scripts can send horse metabolism data.
* Medic scripts can pause metabolism while the player is hospitalized.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-Metabolism
```

Keep the resource folder name exactly:

```text
SS-Metabolism
```

### 2. Import SQL

Import:

```text
EXTRA/ss_metabolism.sql
```

The table is:

```text
ss_metabolism
```

It stores character ID, saved metabolism values, HUD positions, HUD scale, and hidden HUD icons.

If you already had the table before this HUD editor version, run this once:

```sql
ALTER TABLE `ss_metabolism` MODIFY `opt` TEXT DEFAULT NULL;
```

This gives enough space for positions, scale, and hidden icon settings.

### 3. Start Order

Recommended start order:

```cfg
ensure oxmysql
ensure SS-Core
ensure SS-Metabolism
```

If you use `pma-voice`, make sure it is also started on your server.

### 4. Restart The Server

After importing SQL and checking start order, restart the server and test the HUD in-game.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main server/client configuration.
* `config.js`: UI thresholds and core max values.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: NUI page.
* `UI/css/css.css`: NUI styling.
* `UI/js/js.js`: NUI logic.
* `EXTRA/ss_metabolism.sql`: Database table.

***

## First Configuration

Open:

```text
config.lua
```

The file is grouped into clear sections. Change values, not logic.

### General Settings

```lua
Dev = true
WaitBeforeLoad = 10
CommandSetHud = "sethud"
ToggleHud = "shud"
Refresh = 20
SaveRefresh = 60
ClockMode = "analog"
```

* `Dev`: Use `true` while testing. Use `false` on live servers.
* `WaitBeforeLoad`: Seconds before HUD loads after character selection.
* `CommandSetHud`: Command used to edit the HUD.
* `ToggleHud`: Command used to show/hide the HUD.
* `Refresh`: Main metabolism tick in seconds.
* `SaveRefresh`: Minimum seconds between database saves.
* `ClockMode`: `"analog"` or `"digital"`.

***

## UI Thresholds

Open:

```text
config.js
```

Example:

```js
CONFIG = {
    MaxHealth: 60,
    MaxStamina: 60,
    Hungry: 20,
    Thirsty: 20,
    Stress: 80,
    Dirtiness: 80,
};
```

* `MaxHealth` and `MaxStamina`: Max outer core shown by the UI.
* `Hungry`, `Thirsty`, `Health`, and `Stamina`: Blink when below the configured value.
* `Stress` and `Dirtiness`: Blink when above the configured value.
* Horse values follow the same rule for horse HUD icons.

***

## HUD Editor

Players can use:

```text
/sethud
```

This opens HUD edit mode.

In edit mode players can:

* Drag HUD icons.
* Change HUD scale with `+` and `-`.
* Hide/show every HUD icon with switches.
* Press `ESC` to save and close.

Saved settings are stored in the `opt` column in `ss_metabolism`.

If no saved position exists, the HUD uses the default bottom-centered layout.

### HUD Toggle

Players can use:

```text
/shud
```

This hides or shows the full HUD.

***

## Initial Player Values

```lua
Initial = {
    Thirsty = 90,
    Hungry = 75,
    Stress = 10,
    Reputation = 100,
}
```

These values are used when a character has no saved metabolism data yet.

***

## Player Health & Stamina Cores

```lua
UseHealthStamina = true
```

If enabled, the script shows custom player health and stamina cores.

The UI uses:

* `UI/img/health`
* `UI/img/stamina`
* `UI/img/meter`

The outer core respects `MaxHealth` and `MaxStamina` from `config.js`.

***

## Horse HUD

```lua
UseHorseHealthStamina = true
HorseStats = true
HorseMetabolism = {
    Thirsty = 1,
    Hungry = 1,
}
```

* `UseHorseHealthStamina`: Shows horse health/stamina cores.
* `HorseStats`: Shows horse hunger/thirst.
* `HorseMetabolism`: Values removed every `Refresh` tick.

Horse stats appear when the player is mounted or when external horse data is sent to the script.

***

## Temperature

```lua
Temperature = {3, 35}
```

* First number: Minimum safe temperature.
* Second number: Maximum safe temperature.

Clothing can add warmth:

```lua
TemperatureSettings = {
    ["HAT"] = 1,
    ["SHIRT"] = 2,
    ["COAT"] = 5,
}
```

If the final player temperature is too low or too high, the script can affect hunger, thirst, and stress.

***

## Metabolism Decrease

```lua
Metabolism = {
    ["Idle"] = {Thirsty = 0.4, Hungry = 0.3, Stress = 0},
    ["Running"] = {Thirsty = 1.0, Hungry = 0.8, Stress = 0},
    ["Combat"] = {Thirsty = 1.2, Hungry = 1.2, Stress = 5},
}
```

* `Thirsty`: Removed from thirst.
* `Hungry`: Removed from hunger.
* `Stress`: Added to stress. Negative values remove stress.

These values apply every `Config.Refresh` tick.

***

## Low Hunger / Low Thirst Effects

```lua
MetabolismMin = 20
MetabolismStats = {
    ["THIRSTY"] = {Health = 30, Stamina = 10, Stress = 5},
    ["HUNGRY"] = {Health = 25, Stamina = 5, Stress = 5},
}
```

If hunger or thirst goes below `MetabolismMin`, the script can damage health, reduce stamina, and increase stress.

If the player is hospitalized through the medic state, metabolism decrease is paused.

***

## Stress Effects

```lua
StressRagdoll = true
RagDollObjects = true
RagDollObjectsChance = 85
DecreaseFasterStamina1 = 1.5
DecreaseFasterStamina2 = 2.0
```

High stress can make stamina drain faster and can trigger ragdoll behavior if enabled.

***

## Reputation

```lua
RepStats = true
ActiveNpcHate = true
RadiusNpc = 20.0
```

Reputation is stored internally from `0` to `1000`.

The export:

```lua
exports["SS-Metabolism"]:GetRep()
```

returns a reputation level from `0` to `10`.

Very low reputation can make NPCs walk away, run away, or become aggressive depending on config.

***

## Housing HUD

The script can show a housing icon and a small number badge.

External scripts can call:

```lua
exports["SS-Metabolism"]:SetHousing(mode, number)
```

Modes:

* `0`: White/default.
* `1`: Green.
* `2`: Red.

Example:

```lua
exports["SS-Metabolism"]:SetHousing(1, 25)
```

To change the icon:

```lua
exports["SS-Metabolism"]:HousingIcon("stash")
```

***

## Voice / Microphone HUD

The microphone HUD uses RedM mumble talking status:

```lua
MumbleIsPlayerTalking(PlayerId())
```

Voice range is read from:

```lua
LocalPlayer.state.proximity
```

This works with pma-voice style proximity state.

***

## Clock HUD

The HUD supports:

```lua
ClockMode = "analog"
```

or:

```lua
ClockMode = "digital"
```

The clock updates only when Lua sends a sync to NUI. It does not run its own JavaScript time loop.

***

## Usable Goods / Items

Items are configured in:

```lua
Config.Goods
```

Example:

```lua
["apple"] = {
    Label = "Mar",
    Mode = "EAT",
    Prop = "p_apple01x",
    Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
    Times = 1,
    Alcohol = false,
    Effect = false,
    OverPowerStamina = false,
    OverPowerHealth = false,
}
```

Important fields:

* `Label`: Item label used in messages.
* `Mode`: Animation/action type.
* `Prop`: Prop model attached during use. Use `false` to disable.
* `Metabolism.hunger`: Adds hunger.
* `Metabolism.thirsty`: Adds thirst.
* `Metabolism.stress`: Adds stress. Use a negative value to remove stress.
* `Metabolism.health`: Heals player or `false`.
* `Metabolism.stamina`: Restores stamina or `false`.
* `Times`: How many uses/sips/bites before finished.
* `Alcohol`: Drunkness amount or `false`.
* `Effect`: PostFX effect table or `false`.
* `OverPowerStamina`: Stamina core overpower duration/value or `false`.
* `OverPowerHealth`: Health core overpower duration/value or `false`.

Supported modes:

* `EAT`
* `DRINK`
* `SMOKE`
* `SYRINGE`
* `BOWL`
* `BOTTLE`
* `BANDAGE`

***

## Add A New Item

Copy an existing item and change only the values:

```lua
["my_food"] = {
    Label = "My Food",
    Mode = "EAT",
    Prop = "p_bread_13_ab_s_a",
    Metabolism = {hunger = 25, thirsty = false, stress = -2, health = false, stamina = false},
    Times = 1,
    Alcohol = false,
    Effect = false,
    OverPowerStamina = false,
    OverPowerHealth = false,
}
```

The item name must also exist in your inventory/items system.

***

## Exports

### Stress

```lua
exports["SS-Metabolism"]:GetStress()
exports["SS-Metabolism"]:AddStress(10)
exports["SS-Metabolism"]:RemoveStress(10)
```

### Thirst

```lua
exports["SS-Metabolism"]:GetThirsty()
exports["SS-Metabolism"]:AddThirsty(20)
exports["SS-Metabolism"]:RemoveThirsty(20)
```

### Hunger

```lua
exports["SS-Metabolism"]:GetHungry()
exports["SS-Metabolism"]:AddHungry(20)
exports["SS-Metabolism"]:RemoveHungry(20)
```

### Reputation

```lua
exports["SS-Metabolism"]:GetRep()
exports["SS-Metabolism"]:AddRep(100)
exports["SS-Metabolism"]:RemoveRep(100)
```

### Horse Hunger

```lua
exports["SS-Metabolism"]:GetHorseHungry()
exports["SS-Metabolism"]:AddHorseHungry(20)
exports["SS-Metabolism"]:RemoveHorseHungry(20)
```

### Horse Thirst

```lua
exports["SS-Metabolism"]:GetHorseThirsty()
exports["SS-Metabolism"]:AddHorseThirsty(20)
exports["SS-Metabolism"]:RemoveHorseThirsty(20)
```

### Housing

```lua
exports["SS-Metabolism"]:SetHousing(1, 25)
exports["SS-Metabolism"]:HousingIcon("stash")
```

***

## Events

### NUI Focus

```lua
TriggerEvent("SS-Metabolism:setNuiFocus", true)
TriggerEvent("SS-Metabolism:setNuiFocus", false)
```

### Disease / Custom Health Icon

```lua
TriggerEvent("SS-METABOLISM:CLIENT:DISEASE", "snakepoison")
```

The image must exist in:

```text
UI/img/health
```

Use this to restore the default health icon:

```lua
TriggerEvent("SS-METABOLISM:CLIENT:DISEASE", "default")
```

### Horse Data

External horse scripts can send:

```lua
TriggerEvent("S!r@#Blu$$-SS-METABOLISM:CLIENT:SENDHORSE", horse, stats)
```

Where `stats` can include:

```lua
{
    thirsty = 100,
    hungry = 100
}
```

### Medical Cabinet / Hospital State

The script listens for:

```lua
TriggerEvent("SS-MedicJob:Client:MedicalCabinet", true)
TriggerEvent("SS-MedicJob:Client:MedicalCabinet", false)
```

When enabled, metabolism decrease/damage is paused.

***

## Database

Table:

```text
ss_metabolism
```

Columns:

* `charid`: Character ID.
* `info`: Saved metabolism data.
* `opt`: Saved HUD settings. Use `TEXT`, because positions, scale, and hidden icons can be longer than 500 characters.

HUD settings can contain:

```json
{
  "scale": 1,
  "hidden": {
    "mic": true
  },
  "ry": {
    "left": 250,
    "top": 900
  }
}
```

***

## Troubleshooting

### HUD Does Not Show

Check:

* Resource name is `SS-Metabolism`.
* `SS-Core` starts before this resource.
* SQL table exists.
* Character selected event is being triggered.
* `Dev = true` if testing without normal character selection.

### HUD Icons Are Top-left

This should no longer happen. If a player has old or broken saved settings, open:

```text
/sethud
```

Move or save again with `ESC`.

### Item Does Not Work

Check:

* Item exists in your inventory/core.
* Item name matches `Config.Goods`.
* `SS-Core` usable registration is working.
* Resource started after `SS-Core`.

### Microphone Icon Does Not Turn Green

Check:

* pma-voice/mumble is running.
* `MumbleIsPlayerTalking` exists in your RedM build.
* `LocalPlayer.state.proximity` exists for voice range.

### Clock Is Not Moving Every Second

This is intentional. The clock updates only on sync from Lua for better fidelity with server time.

### Stress Or Dirtiness Looks Full

This is intended when the value is high:

* Higher value = fuller meter.
* Lower value = emptier meter.

### Database Is Not Saving

Check:

* `oxmysql` is started.
* `ss_metabolism` table exists.
* `charid` is valid.
* `SaveRefresh` is not too high for your test.

***

## Recommended Live Checklist

Before going live, confirm:

* SQL has been imported.
* `oxmysql` starts first.
* `SS-Core` starts before this script.
* Resource folder name is `SS-Metabolism`.
* `Dev = false`.
* `Refresh` is set to a sane value, recommended `10-20+`.
* `SaveRefresh` is set to a sane value, recommended `60+`.
* Item names are checked in `Config.Goods`.
* `/sethud` works.
* `/shud` works.
* Hunger/thirst decrease works.
* Stress effects work.
* Horse HUD works if enabled.
* pma-voice microphone works if used.

