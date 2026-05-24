# Configuration File

## Main Files

SS-Weapons is configured from:

* `config.lua`: Main settings, stores, gunsmith benches, cleaning, repair, wear, HUD, preview sync, poison/tranquilizer, and prices.
* `cfg/weapons.lua`: Weapon catalog.
* `cfg/ammo.lua`: Ammo catalog.
* `l/l.lua`: Lua translations.
* `config.js`: NUI / interface translations and book UI settings.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Weapon store and gunsmith UI.

***

## config.lua

{% code overflow="wrap" %}
```lua
Config = {
    Dev = false,
    Language = "EN",
    PressKey = 0xD9D0E1C0,
    WaitingAnime = true,

    MinLabel = 2,
    MaxLabel = 10,
    PriceForCustomSerial = 1000,
    PriceForCustomLabel = 25,

    CleanWeaponItem = "leather",
    RemoveAfterClean = true,
    CleanWeaponTime = 10000,
    MinCleanWeaponTime = 2500,
    InspectWeaponCommand = "w_inspect",
    DirtyWeaponCommand = "dirtyweapon",

    WeaponHud = {
        Enabled = false,
        Position = "top-right",
        UpdateInterval = 150,
        HideWhenUiOpen = true,
        ImagePath = "img/weapons/%s.png",
        AmmoIconPath = "img/ammo_types/%s.png",
    },

    PreviewSync = {
        Enabled = true,
        Radius = 8.0,
        MaxSpectators = 6,
        CheckInterval = 2000,
    },

    WeaponRepair = {
        Enabled = true,
        Item = "weapon_repair_kit",
        RemoveItem = true,
        RepairAmount = 0.10,
        MinRustRequired = 0.01,
    },

    UseDegradation = true,
}
```
{% endcode %}

***

## General Settings

```lua
Dev = false
Language = "EN"
PressKey = 0xD9D0E1C0
WaitingAnime = true
```

* `Dev`: Enables test/debug commands when `true`. Use `false` on live servers.
* `Language`: Translation table used by the script.
* `PressKey`: Key used to open store and gunsmith prompts.
* `WaitingAnime`: Plays idle animation while the UI is open.

***

## Custom Weapon Label & Serial

```lua
MinLabel = 2
MaxLabel = 10
PriceForCustomSerial = 1000
PriceForCustomLabel = 25
```

* `MinLabel`: Minimum custom weapon label length.
* `MaxLabel`: Maximum custom weapon label length.
* `PriceForCustomSerial`: Extra price for custom serial number.
* `PriceForCustomLabel`: Extra price for custom weapon label.

***

## Weapon HUD

```lua
WeaponHud = {
    Enabled = false,
    Position = "top-right",
    UpdateInterval = 150,
    HideWhenUiOpen = true,
}
```

Position options:

* `top-left`
* `top-center`
* `top-right`
* `middle-left`
* `center`
* `middle-right`
* `bottom-left`
* `bottom-center`
* `bottom-right`

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

* `Enabled`: Enables weapon repair.
* `Item`: Required repair item.
* `RemoveItem`: Removes one item after successful repair.
* `RepairAmount`: Amount of permanent rust/damage removed.
* `MinRustRequired`: Minimum rust required before repair is allowed.

***

## Weapon Wear

```lua
UseDegradation = true

WeaponWear = {
    SaveDirt = true,
    SaveDirtInterval = 10000,
    NativeStatusCacheInterval = 1000,
    SaveLevelDecimals = 4,
    PermanentDamageOnMaxDamage = 0.10,
    PermanentDamageOnClean = 0.02,
}
```

Weapon condition values are stored from `0.0` to `1.0`.

Example:

```text
0.25 = 25%
1.0 = 100%
```

***

## Gunsmith Payment

```lua
WeaponEditPayment = {
    Type = "gold",
}
```

Payment type can be:

* `gold`
* `money`

***

## Stores & Gunsmith Benches

Stores are configured in:

```lua
Config.Stores = {
    [1] = {
        Cover = "coverbook",
        Name = "GunSmith",

        EnableStore = true,
        StoreBlip = 202506373,
        CatalogWeapon = {-281.4826, 780.6805, 119.4771, 187.0176},
        CamStore = {-281.23, 779.84, 120.00, -90.0, -180.0, 0.0, 50.0},
        WichWeapons = false,
        WichAmmo = false,
        Serial = false,
        CustomLabel = false,

        EnableGunsmith = true,
        GunSmithBlip = 1321928545,
        ModifyWeapons = {-277.2002, 778.7532, 119.4539},
        ModifyPos = {-276.20, 778.82, 119.55, 90.0, 180.0, -89.73},
        CamGunSmith = {-276.29, 778.99, 120.00, -90.0, 0.0, -90.0, 80.0},
        Jobs = {"Guvernator", "Manager", "ArmurierVAL", "Armurier"},
    },
}
```

Important fields:

* `EnableStore`: Enables the buy catalog.
* `EnableGunsmith`: Enables the gunsmith bench.
* `WichWeapons`: `false` for all weapons, `{}` for none, or a list of weapon keys.
* `WichAmmo`: `false` for all ammo, `{}` for none, or a list of ammo item keys.
* `Jobs`: Jobs allowed to use the gunsmith bench.

***

## Weapon Catalog

Weapons are configured in:

```text
cfg/weapons.lua
```

Example:

```lua
["WEAPON_REVOLVER_CATTLEMAN"] = {
    Weapon = "WEAPON_REVOLVER_CATTLEMAN",
    Label = "Cattleman Revolver",
    Tittle = "Cattleman Revolver",
    Description = "The Cattleman Revolver is a dependable weapon...",
    Category = "Revolver",
    Price = 50,
    Gold = 0,
    BuyJobs = {},
    BuyJobsGrade = {},
    ModifyJobs = {},
    ModifyJobsGrade = {},
    Typ = "WEAPON",
}
```

***

## Ammo Catalog

Ammo is configured in:

```text
cfg/ammo.lua
```

Example:

```lua
["ammorevolvernormal"] = {
    Item = "ammorevolvernormal",
    Label = "Revolver Normal Ammo",
    Category = "Ammo",
    Price = 50,
    Gold = 0,
    Type = "AMMO_REVOLVER",
    MaxAmmo = 200,
    Amount = 100,
}
```

* `Type`: Ammo type added to the player belt.
* `MaxAmmo`: Maximum ammo allowed in the belt.
* `Amount`: Bullets added by one ammo box.
