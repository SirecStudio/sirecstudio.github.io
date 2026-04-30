# Configuration Helps

## SS-Stable Setup & Configuration Guide

SS-Stable is an advanced stable system for RedM. It handles personal horses, personal wagons, horse and wagon shops, equipment, training, breeding, taming, wagon cargo, repairs, animal cargo, markets, and optional integrations with other Sirec Studio scripts.

This guide is written for server owners who want to install, configure, and test the script safely, even without deep Lua knowledge.

***

## Features Overview

SS-Stable includes:

* Personal horse ownership: buy, store, call, and send away horses.
* Personal wagon ownership: buy, store, call, and send away wagons.
* Horse and wagon equipment shops.
* Horse and wagon preview inside stable zones.
* Horse equipment transfer using the `horseequipment` item.
* Horse food, water, tricks, pelts, and saddlebag inventory.
* Horse training, experience, horseshoes, and stamina behavior.
* Breeding, foals, age stages, and optional crossbreed visuals.
* Wild horse taming and selling.
* Player horse market and stable budget withdrawal.
* Wagon cargo for hunted animals and pelts.
* Wagon damage, repair, cargo blocking, and stash blocking when damaged.
* Multi-language support.
* Optional integrations with `SS-Clan`, `SS-Housing`, `SS-Metabolism`, lockpick systems, and outfit menus.

***

## Dependencies

### Required

* `SS-Core`
* `oxmysql`

### Used By Default

* `menuapi`
* `vorp_core`, used by the default `NOTIFY(text)` function.
* `SS-Inputs`, used for keyboard input prompts.

### Optional Integrations

* `SS-Clan`
* `SS-Housing`
* `SS-Metabolism`
* `SS-Lockpick`
* `outfits`, or another outfit menu trigger.

If you do not use an optional integration, disable it in `config.lua`.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-Stable
```

Keep the resource folder name exactly:

```text
SS-Stable
```

### 2. Import SQL

Import the SQL file from:

```text
EXTRA/ss_stable.sql
```

The main database tables are:

* `horses`
* `wagons`

The `horses` table stores ownership data, selected horse state, model, name, components, equipment, stats, shoes, age, breeding data, carried pelts, horse status, packed property data, and crossbreed values.

The `wagons` table stores ownership data, selected wagon state, model, name, components, damage/body data, cargo data, and stored city or area.

### 3. Add Inventory Items

Check every item name enabled in your config and make sure it exists in your inventory/database.

Important examples:

```lua
HorseEquipmentItem = "horseequipment"
ReviveItem = "horserevive"
HammerRepair = "ironhammer"
HammerRepairNeeds = {"nails", 4, "Cuie"}
```

If an item does not exist, the feature using that item will not work correctly.

### 4. Start Order

Recommended start order:

```cfg
ensure oxmysql
ensure SS-Core
ensure SS-Stable
```

If you use optional integrations, start them before `SS-Stable` when possible:

```cfg
ensure SS-Clan
ensure SS-Housing
ensure SS-Metabolism
ensure SS-Stable
```

### 5. Restart The Server

After importing SQL and checking the start order, restart the server and test the main stable flow in-game.

***

## Languages

Languages are configured in:

```text
l/l.lua
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

Example:

```lua
Language = "RO"
```

***

## First Configuration

Open:

```text
config.lua
```

The file is grouped into clear sections:

* General settings
* Controls
* Horse extra equipment
* Horse settings
* Wagon settings
* Training
* Breeding
* Taming
* Stable locations
* Notification function

### General Settings

```lua
Dev = true
Language = "EN"
Metabolism = false
WebHook = ""
```

* `Dev`: Use `true` while testing. Use `false` on live servers so the script waits for character selection.
* `Language`: Translation language used by the script.
* `Metabolism`: Set to `true` only if you use `SS-Metabolism`.
* `WebHook`: Discord webhook URL. Leave empty to disable webhook logs.

### Police & Search Settings

```lua
SearchAllow = {"Maresal", "Judecator"}
SearchAllowGrade = 4
GradePolice = 9
```

* `SearchAllow`: Jobs allowed to search horses and wagons with fewer restrictions.
* `SearchAllowGrade`: Minimum grade required for those jobs.
* `GradePolice`: Grade allowed to take market horses for free, useful for stolen horse recovery.

### Controls

Controls use RedM key hashes:

```lua
CallHorse = 0x24978A28
CallWagon = 0xF3830D8E
HorseOpenStash = 0xE30CD707
WagonOpenStash = 0xFF8109D8
```

Only change these values if you know the correct RedM control hash.

***

## Horse Systems

### Horse Equipment Transfer Item

SS-Stable supports one item that can store the main tack from one horse and apply it to another personal horse:

```lua
HorseEquipmentItem = "horseequipment"
```

Behavior:

* The player must be inside a stable area.
* The source horse must be a personal horse.
* The item stores main horse equipment as metadata.
* The item can apply that equipment to another personal horse.
* Mane, tail, mustache, and extra equipment are not included.
* Equipment cannot be applied to a horse that already has main equipment.

The item must exist in your inventory/database.

### Block Mount Without Saddle

```lua
BlockMount = true
```

* `true`: Managed horses without saddle/equipment cannot be mounted normally.
* `false`: Players can mount even if the horse has no equipment.

This helps prevent players from removing equipment only to protect saddlebag access while travelling.

### Extra Horse Equipment

Example:

```lua
ExtraEquip = {
    ["horseblanket"] = {Hash = 0x9F275113, Label = "Blanket"},
    ["horselantern"] = {Hash = 0xF08D4D50, Label = "Lantern"},
}
```

Fields:

* The key, for example `horseblanket`, is the usable item name.
* `Hash`: Metaped outfit hash applied to the horse.
* `Label`: Text shown in the menu.
* `Stash`: Optional extra inventory size behavior.
* `Flame`: Optional special visual behavior.

### Core Horse Settings

Important examples:

```lua
MaxHorses = 5
TrainersMaxHorses = 8
BuyHorseAge = {10, 25}
AttackEnemies = 3500
StandbySit = 60
CallHorseOnlyInCities = false
SendHorseOnlyInCities = false
```

* `MaxHorses`: Normal player horse limit.
* `TrainersMaxHorses`: Horse trainer limit.
* `BuyHorseAge`: Random age range for newly bought horses.
* `AttackEnemies`: Minimum EXP required for the horse to attack enemies when called. Use `false` to disable.
* `StandbySit`: Idle time before horses sit/rest. Use `false` to disable.
* `CallHorseOnlyInCities`: Restrict horse calling to allowed cities or stables.
* `SendHorseOnlyInCities`: Restrict sending horses away to allowed cities or stables.

### Horse Food

Example:

```lua
Feed = {
    ["corn"] = {label = "Porumb", boost = false, health = 30, stamina = 10, thirsty = 10, hungry = 45},
}
```

* The key is the item name.
* `label`: Display name.
* `boost`: Enables stronger effect behavior.
* `health`: Horse health restored.
* `stamina`: Horse stamina restored.
* `thirsty` and `hungry`: Used with metabolism integration.

### Horse Tricks

Example:

```lua
HorseTricksCommand = "tricks"
HorseTrickDistance = 15
HorseTricks = {
    [1] = {Tittle = "Pasture", Anim = "base", Dict = "amb_creature_mammal@world_horse_grazing@base", Time = 30000, Flag = 0, Exp = 500},
}
```

* `HorseTricksCommand`: Command used to open tricks. Use `false` to disable command access.
* `HorseTrickDistance`: Maximum distance between player and horse.
* `Exp`: Minimum horse EXP required for that trick.

***

## Wagon Systems

### Core Wagon Settings

Important examples:

```lua
WagonLowHealth = 100
BlockWagonIfDamage = true
ActiveLastPosition = true
CallWagonOnlyInCities = true
SendWagonOnlyInCities = true
WagonDistanceToRoads = 100.0
```

* `WagonLowHealth`: Health threshold where the wagon is considered heavily damaged.
* `BlockWagonIfDamage`: Use `false` to disable blocking, `true` to block under 500 health, or a number such as `300` for a custom threshold.
* `ActiveLastPosition`: Wagon can be recalled only from its saved area.
* `CallWagonOnlyInCities`: Restrict wagon calls to cities, stables, housing areas, or clan areas.
* `SendWagonOnlyInCities`: Restrict sending wagons away.
* `WagonDistanceToRoads`: Road search distance when spawning wagons.

### Wagon Repair

```lua
HammerRepair = "ironhammer"
HammerRepairScenario = "PROP_HUMAN_REPAIR_WAGON_WHEEL_ON_LARGE"
HammerRepairTime = 5000
HammerAddWagonHealth = 250
HammerRepairNeeds = {"nails", 4, "Cuie"}
```

* `HammerRepair`: Usable repair item.
* `HammerRepairScenario`: Scenario played while repairing.
* `HammerRepairTime`: Repair duration in milliseconds.
* `HammerAddWagonHealth`: Health added per repair.
* `HammerRepairNeeds`: Required item, amount, and display label.

### Optional Wagon Integrations

```lua
EnableOutfits
SSHousing = false
SSClan = false
```

* `EnableOutfits`: Event/trigger used to open wardrobe from wagon. Use `false` to disable.
* `SSHousing`: Set to `true` only if you use `SS-Housing`.
* `SSClan`: Set to `true` only if you use `SS-Clan`.

***

## Training, Breeding & Taming

### Training

Training is split into:

* Experience tiers
* Trainer jobs
* Training routes
* Random action training
* Free training
* Horseshoes

Trainer job example:

```lua
Training = {
    Jobs = {"HorseTrainerBW", "HorseTrainerRH", "HorseTrainerSD", "HorseTrainerVAL"},
    Whip = "horsetrain",
    TrainerBookItem = "horselist",
}
```

### Horseshoes

```lua
Shoes = {
    ["ironhorseshoe"] = {label = "Iron Horseshoe", km = 20000},
}
```

* The key is the item name.
* `label`: Display name shown to players.
* `km`: Distance before horseshoe degradation.

### Breeding

```lua
Breeding = {
    Jobs = {"HorseTrainerBW", "HorseTrainerRH"},
    AllowCross = true,
    Pill = "breedpills",
    Brush = "horsebrush",
    Chance = 50,
    BreedWaitTime = 10,
}
```

* `Jobs`: Jobs allowed to breed horses.
* `AllowCross`: Enables custom crossbreed visual values.
* `Pill`: Item used to start breeding.
* `Brush`: Item used to clean horses.
* `Chance`: Chance to start breeding.
* `BreedWaitTime`: Days until the foal is born.

Foal age stages:

```lua
StartRiding = 4
StartBreeding = 6
StartTraining = 8
StartAdult = 10
StartOld = 75
StartDead = 95
StartDeleteIt = 100
```

These values control when foals can be ridden, trained, equipped, become old, die, or are deleted.

### Taming

```lua
Taming = {
    MaxFails = 2,
    MaxSucces = 6,
    RandomTime = {500, 2500},
    ReactionTime = 800,
    TamingPrice = 70,
    SellPrice = 3,
    TamingAge = {20, 30},
}
```

* `MaxFails`: Failed button prompts before taming fails.
* `MaxSucces`: Successful prompts required.
* `RandomTime`: Random time between prompts.
* `ReactionTime`: Time allowed to press the correct prompt.
* `TamingPrice`: Price percentage needed to keep a tamed horse.
* `SellPrice`: Price percentage used when selling a tamed horse.
* `TamingAge`: Random age range for tamed horses.

***

## Stable Locations

Stable entries are configured in `config.lua`.

Example:

```lua
Stables = {
    ["1"] = {
        Name = "Valentine",
        CamPos = {-382.25, 769.90, 118.45},
        Blip = -1456209806,
        MySpot = {-369.63, 791.50, 115.08, -175.34},
        ActiveMyWagon = true,
        MyWagonSpot = {-363.76, 775.34, 115.27, -85.71},
        CustomPos = {-377.70, 770.03, 115.10, 5.11},
        TrainingType = 1,
        TrainingPos = {-393.43, 777.83, 115.60},
        Distance = 15,
        SellHorses = true,
        SellSpots = {
            [1] = {Pos = {-366.33, 782.82, 115.09, 1.53}},
        },
        SellWagons = true,
        SellWagonsSpot = {-377.54, 774.32, 116.09, -86.04},
        SellPlayersHorse = true,
        SellPlayersHorseSpot = {-372.02, 782.51, 115.09, 1.53},
    },
}
```

Important fields:

* `Name`: Stable name.
* `CamPos`: Camera position for UI/preview.
* `Blip`: Stable blip hash or `false`.
* `MySpot`: Personal horse spawn spot.
* `ActiveMyWagon`: Enables personal wagon spot.
* `MyWagonSpot`: Personal wagon spawn spot.
* `CustomPos`: Equipment/customization position.
* `TrainingType`: Training type used at this stable.
* `TrainingPos`: Training, breeding, and taming area.
* `Distance`: Zone radius.
* `SellHorses`: Enables horse shop.
* `SellSpots`: Horse shop preview spot.
* `SellWagons`: Enables wagon shop.
* `SellWagonsSpot`: Wagon shop preview spot.
* `SellPlayersHorse`: Enables player horse market.
* `SellPlayersHorseSpot`: Player horse market spot.

Keep interaction spots separated. If two spots overlap, prompts can overlap in-game.

### Add A New Stable

Copy an existing stable entry and change only the values:

```lua
["6"] = {
    Name = "Strawberry Stable",
    CamPos = {-1810.0, -560.0, 158.0},
    Blip = -1456209806,
    MySpot = {-1815.0, -558.0, 156.0, 90.0},
    ActiveMyWagon = true,
    MyWagonSpot = {-1820.0, -560.0, 156.0, 90.0},
    CustomPos = {-1812.0, -562.0, 156.0, 90.0},
    TrainingType = 3,
    TrainingPos = {-1830.0, -570.0, 156.0},
    Distance = 15,
    SellHorses = true,
    SellSpots = {
        [1] = {Pos = {-1816.0, -555.0, 156.0, 90.0}},
    },
    SellWagons = true,
    SellWagonsSpot = {-1824.0, -558.0, 156.0, 90.0},
    SellPlayersHorse = true,
    SellPlayersHorseSpot = {-1818.0, -552.0, 156.0, 90.0},
},
```

After adding a stable, restart the resource/server and test every interaction spot.

***

## Adding Shop Content

### Add A New Horse

Open:

```text
cfg/horses.lua
```

Copy an existing horse entry in the correct category and change:

```lua
{
    Model = "a_c_horse_morgan_bay",
    Breed = "Morgan Bay",
    Category = "Morgan",
    PriceMoney = 100,
    PriceGold = 0,
    Description = "Basic riding horse.",
    Stats = {3, 3, 3, 3, 3},
    Crossbreed = 0,
}
```

Important:

* `Model` must be a valid RedM/RDR2 horse model.
* `Stats` order must match the script's expected horse stat order.
* `Crossbreed = 0` means default/no custom crossbreed.

### Add A New Wagon

Open:

```text
cfg/wagons.lua
```

Copy an existing wagon entry and change:

```lua
{
    Model = "cart01",
    Label = "Small Cart",
    PriceMoney = 150,
    PriceGold = 0,
    Description = "Small utility cart.",
    Stash = 50,
    UtilityStash = 0,
}
```

Important:

* `Model` must be a valid wagon/vehicle model.
* `Stash` controls stash capacity.
* `UtilityStash` is used by utility/inventory logic if supported.

### Add Horse Equipment

Open:

```text
cfg/horsesequip.lua
```

Use an existing entry as a template. Equipment categories can include saddle, bags, bedroll, blanket, stirrups, bridles, and other tack parts.

Typical equipment fields:

```lua
{
    Label = "Simple Saddle",
    PriceMoney = 50,
    PriceGold = 0,
    Hash = 0x12345678,
    Category = 1,
    Stats = {speed = 0, stamina = 0, health = 0, acc = 1, handling = 0},
}
```

Important:

* Use valid component hashes.
* Keep equipment order logical: blanket before saddle, saddle before bags.
* Test preview and called horses after adding new equipment.

### Add Wagon Equipment

Open:

```text
cfg/wagonsequip.lua
```

Copy an existing color, livery, or prop entry and change values carefully.

### Add Animal Cargo

Open:

```text
cfg/animals.lua
```

Animals and pelts must use correct model/hash and quality data. If quality data is wrong, players can see the wrong star quality when putting or removing animals from wagons.

***

## Exports

### Get Nearby Horse

```lua
local horse = exports["SS-Stable"]:GetHorse()
```

Returns nearby horse data, or `false`/`nil`.

### Get Nearby Wagon

```lua
local wagon = exports["SS-Stable"]:GetWagon()
```

Returns nearby wagon data, or `false`/`nil`.

### Get Active Personal Wagon

```lua
local myWagon = exports["SS-Stable"]:GetMyWagon()
```

Returns active personal wagon data, or `false`.

### Add Horse EXP

```lua
local added = exports["SS-Stable"]:AddHorseExp(50)
```

Returns:

* `true` if a nearby horse was found and EXP was sent to the server.
* `false` if no valid horse was nearby.

***

## Commands

Player-facing command:

```text
/tricks
```

The command name depends on:

```lua
HorseTricksCommand = "tricks"
```

Dev/test commands can exist when `Config.Dev = true`. They are for testing only and should not be used on live servers.

***

## Notifications

At the bottom of `config.lua`:

```lua
function NOTIFY(text)
    local VORPCore = exports.vorp_core:GetCore()
    VORPCore.NotifyLeft(Config.Texts["tittle_notification"], text, "generic_textures", "tick", 5000, "COLOR_WHITE")
end
```

If your server uses another notification system, change only this function.

***

## Recommended Live Checklist

Before going live, confirm:

* SQL has been imported.
* `SS-Core` starts before `SS-Stable`.
* `Dev = false`.
* `Language` is selected.
* Optional integrations are disabled if missing.
* Inventory items are added.
* Horse shop works.
* Wagon shop works.
* Personal horse call/send works.
* Personal wagon call/send works.
* Horse equipment buying works.
* `horseequipment` item works.
* Wagon repair works.
* Wagon cargo works with different animal qualities.
* Horse training works.
* Breeding works.
* Taming works.

***

## Troubleshooting

### Stable Menu Does Not Appear

Check:

* Resource name is `SS-Stable`.
* `SS-Core` is started.
* `Config.Dev` is correct for your test/live flow.
* Player has selected a character.
* Stable coordinates are correct.
* Spots are not too far away or inside the ground.

### UI Opens But Stats Look Wrong

Check:

* Horse/wagon data in the database.
* `cfg/horses.lua` stats.
* Equipment stats.
* Browser cache or NUI refresh.

### Horse Does Not Spawn

Check:

* Horse model exists.
* Player is in an allowed call area.
* `CallHorseOnlyInCities`.
* `AllowedToCallCity`.
* Server/client console for model load timeout.

### Wagon Does Not Spawn

Check:

* Wagon model exists.
* Player is in an allowed call area.
* `CallWagonOnlyInCities`.
* `WagonDistanceToRoads`.
* `ActiveLastPosition`.
* `SS-Clan` and `SS-Housing` settings if used.

### Cannot Open Wagon Stash Or Cargo

Check:

* Wagon health.
* `BlockWagonIfDamage`.
* `WagonLowHealth`.
* Lockpick blacklist cities.
* Police/search permissions.

### Cannot Mount Horse

Check:

* `BlockMount`.
* Horse has saddle/equipment.
* Horse is old enough.
* Horse is not dead.

### Horse Equipment Item Does Not Work

Check:

* Item `horseequipment` exists in inventory/database.
* Player is inside a stable area.
* Horse is a personal horse.
* Target horse has no main equipment.
* Metadata is preserved by your inventory framework.

### Horse Food Does Not Work

Check:

* Item exists.
* Item is registered as usable server-side.
* Horse is nearby.
* `Feed` config entry exists.

### Wagon Repair Does Not Work

Check:

* `HammerRepair` item exists.
* Player is near the active wagon.
* Required repair items exist.
* Wagon has draft animals if your config/logic requires it.
* Wagon is not below recovery threshold.

### Translations Show Nil Or Wrong Text

Check:

* `Language`.
* `l/l.lua`.
* Missing translation keys.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature.
* `false` disables a feature.
* Numbers do not use quotes: `100`.
* Item names usually use quotes: `"itemname"`.
* Coordinates usually look like `{x, y, z, heading}`.

Bad:

```lua
MaxHorses = "5"
```

Good:

```lua
MaxHorses = 5
```

Bad, if you do not actually use `SS-Housing`:

```lua
SSHousing = true
```

Good:

```lua
SSHousing = false
```

***

## Support

For bug reports and support:

```text
https://discord.gg/9XNBaQSmMd
```
