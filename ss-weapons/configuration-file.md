# Configuration File

## Main Files

SS-Weapons is configured from:

* `config.lua`: Main settings, stores, gunsmith benches, editor camera, cleaning, repair, wear, HUD, preview sync, poison / tranquilizer and prices.
* `cfg/weapons.lua`: Weapon catalog.
* `cfg/ammo.lua`: Ammo catalog.
* `cfg/anchors.lua`: Where the editor callout lines start on each weapon type.
* `cfg/presets.json`: Per-weapon camera and callout presets saved from the Dev panel (JSON, written by the server).
* `l/l.lua`: Lua notifications translations.
* `config.js`: UI language and UI options.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`, `UI/css/css.css`, `UI/js/js.js`, `UI/js/design.js`: Catalogue and gunsmith UI.

***

## config.lua

{% code overflow="wrap" %}
```lua
Config = {
    Dev = false,
    Language = "EN",
    PressKey = 0xD9D0E1C0,
    WaitingAnime = true,

    InventoryVersion = "auto",          -- "auto" | "v1" | "v2"
    InventoryDegradationHandled = false,

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

    GunsmithEditor = {
        ZoomStep = 6.0,
        MinFov = 22.0,
        MaxFov = 95.0,
        AnchorUpdateInterval = 120,
        ShowAnchorDots = true,
        AutoCenter = true,
        AutoFit = true,
        FitWidth = 0.5,
        FitHeight = 0.55,
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

    WeaponEditPayment = { Type = "gold" },
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

* `Dev`: Enables the test commands and the **Weapon preset** panel in the editor when `true`. Keep `false` on live servers.
* `Language`: Notification language (set the same value in `config.js` for the UI).
* `PressKey`: Key used to open store and gunsmith prompts.
* `WaitingAnime`: Plays an idle animation while the UI is open.

***

## Inventory Version

```lua
InventoryVersion = "auto"
InventoryDegradationHandled = false
```

* `InventoryVersion`: `"auto"` detects vorp\_inventory v1 / v2 from the `loadout` table (recommended); `"v1"` or `"v2"` forces it. Each version has its own equip logic on the client.
* `InventoryDegradationHandled`: vorp\_inventory v2 ships its own weapon degradation. Set `USE_WEAPON_DEGRADATION = false` in the inventory config (and `USE_WEAPON_COMPONENTS = false`), then set this to `true` to silence the startup warning.

***

## Custom Weapon Label & Serial

```lua
MinLabel = 2
MaxLabel = 10
PriceForCustomSerial = 1000
PriceForCustomLabel = 25
```

* `MinLabel` / `MaxLabel`: Custom weapon name length (max 10).
* `PriceForCustomSerial`: Extra price for a custom serial number.
* `PriceForCustomLabel`: Extra price for a custom weapon name.

Whether a store offers these options is set per store with `Serial` and `CustomLabel` (see Stores).

***

## Cleaning & Inspection

```lua
CleanWeaponItem = "leather"
RemoveAfterClean = true
CleanWeaponTime = 10000
MinCleanWeaponTime = 2500
InspectWeaponCommand = "w_inspect"
DirtyWeaponCommand = "dirtyweapon"
```

* `CleanWeaponItem`: Usable item that starts the inspection / cleaning flow.
* `RemoveAfterClean`: Removes one item after a successful clean.
* `CleanWeaponTime` / `MinCleanWeaponTime`: Cleaning duration in ms, scaled by how dirty the weapon is.
* `InspectWeaponCommand`: Command that opens the inspection; `w_inspectstatus` and `w_inspectreset` are always available for diagnostics.
* `DirtyWeaponCommand`: Dev-only test command.

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

Position options: `top-left`, `top-center`, `top-right`, `middle-left`, `center`, `middle-right`, `bottom-left`, `bottom-center`, `bottom-right`. Images come from `UI/img/weapons` and `UI/img/ammo_types`.

***

## Gunsmith Editor

```lua
GunsmithEditor = {
    ZoomStep = 6.0,
    MinFov = 22.0,
    MaxFov = 95.0,
    AnchorUpdateInterval = 120,
    ShowAnchorDots = true,
    AutoCenter = true,
    AutoFit = true,
    FitWidth = 0.5,
    FitHeight = 0.55,
}
```

* `ZoomStep`, `MinFov`, `MaxFov`: Zoom buttons of the editor.
* `AnchorUpdateInterval`: Milliseconds between callout line updates.
* `ShowAnchorDots`: Draws a brass ring where each callout line touches the weapon.
* `AutoCenter`: Slides the preview so the middle of the weapon model sits under the bench camera.
* `AutoFit`: Zooms until the weapon spans `FitWidth` of the screen width (`FitHeight` when it stands upright).

***

## Callout Anchors & Presets

`cfg/anchors.lua` places every part on the weapon as a fraction of the model's bounding box, per weapon type (`SHORTARM`, `LONGARM`, `SHOTGUN`, `MELEE`):

```lua
Config.Anchors = {
    Auto = {
        Enabled = true,
        UseBones = true,
        MuzzleAtPositiveEnd = true,
        SideSign = 1,
        Fractions = {
            LONGARM = {
                SIGHT  = {0.96,  0.55}, -- {t: 0 rear .. 1 muzzle, h: -1 trigger side .. +1 sights side}
                BARREL = {0.74,  0.25},
                -- ...
            },
        },
    },
    Weapons = {}, -- optional per-weapon overrides in metres {right, forward, up}
}
```

* `SideSign = -1` if the sights end up on the trigger side; `MuzzleAtPositiveEnd = false` if a weapon without a muzzle bone is mirrored.

`cfg/presets.json` holds per-weapon camera and anchor tuning saved from the Dev panel (Save preset). Ship it with the resource. It can also be edited by hand:

```json
{
  "WEAPON_SNIPERRIFLE_CARCANO": {
    "camera": {"fov": 46.0, "panX": 0.05, "yaw": 3.0},
    "anchors": {"SCOPE": [0.0, 0.12, 0.06]}
  }
}
```

Camera keys: `panX`, `panY`, `dolly`, `yaw`, `pitch`, `fov`, `spin` (turns the weapon on the bench). Anchor values are `{right, forward, up}` in metres.

***

## Preview Sync

```lua
PreviewSync = {
    Enabled = true,
    Radius = 8.0,
    MaxSpectators = 6,
    CheckInterval = 2000,
}
```

Nearby players inside `Radius` see the preview weapon while someone edits it. A bench is locked to one player at a time.

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

* `Enabled`: Shows the Repair button in the editor.
* `Item`: Required repair item (empty = no item needed).
* `RemoveItem`: Removes one item after a successful repair.
* `RepairAmount`: Permanent wear removed (0.10 = 10%).
* `MinRustRequired`: Minimum permanent wear before repair is allowed.

***

## Weapon Wear

```lua
UseDegradation = true

WeaponWear = {
    SaveDirt = true,
    SaveDirtInterval = 10000,
    NativeStatusCacheInterval = 1000,
    SaveLevelDecimals = 4,
    EquipApplyDelay = 1500,
    EquipApplyAttempts = 10,
    EquipApplyAttemptDelay = 300,
    EquipVerifyDelay = 3000,
    PermanentDamageOnMaxDamage = 0.10,
    PermanentDamageOnClean = 0.02,
    CleanDirtLevel = 0.0,
    CleanSootLevel = 0.0,
    CleanDegradationLevel = 0.0,
}
```

Values are stored from `0.0` to `1.0` (`0.25 = 25%`). `UseDegradation = true` lets permanent wear make a weapon unusable at 100%. The server only accepts wear that grows; cleaning lowers dirt / soot / degradation and repair lowers permanent wear.

***

## Gunsmith Payment & Prices

```lua
WeaponEditPayment = { Type = "gold" } -- "gold" or "money"

GunSmith = {
    ["SKIN"] = 250,
    ["SCOPE"]    = { ["COMP"] = 0.5, ["MATERIAL"] = 10, ["ENGRAVE"] = 10, ["ENGRAVEM"] = 10 },
    ["TRIGGER"]  = { ["MATERIAL"] = 10, ["ENGRAVE"] = 10, ["ENGRAVEM"] = 10 },
    ["SIGHT"]    = { ["COMP"] = 30, ["MATERIAL"] = 15, ["ENGRAVE"] = 15, ["ENGRAVEM"] = 15 },
    ["HAMMER"]   = { ["MATERIAL"] = 15, ["ENGRAVE"] = 15, ["ENGRAVEM"] = 15 },
    ["BARREL"]   = { ["MATERIAL"] = 30, ["ENGRAVE"] = 15, ["ENGRAVEM"] = 15 },
    ["CYLINDER"] = { ["MATERIAL"] = 35, ["ENGRAVE"] = 15, ["ENGRAVEM"] = 15 },
    ["GRIP"]     = { ["COMP"] = 45, ["MATERIAL"] = 20, ["ENGRAVE"] = 20, ["ENGRAVEM"] = 20, ["TINT"] = 20 },
    ["BODY"]     = { ["MATERIAL"] = 50, ["ENGRAVE"] = 25, ["ENGRAVEM"] = 25, ["TINT"] = 25 },
    ["WRAP"]     = { ["COMP"] = 55, ["MATERIAL"] = 30, ["ENGRAVE"] = 25, ["ENGRAVEM"] = 25, ["TINT"] = 25 },
    ["CLIP"]     = { ["COMP"] = 25, ["MATERIAL"] = 10, ["ENGRAVE"] = 10, ["ENGRAVEM"] = 10, ["TINT"] = 10 },
    ["CYLINDER_TINT"] = { ["COMP"] = 20 }, -- bow frame colour
    ["BARREL_TINT"]   = { ["COMP"] = 20 }, -- bow grip colour
    ["TRIGGER_TINT"]  = { ["COMP"] = 20 }, -- bow string colour
}
```

* `COMP`: Physical component. `MATERIAL`: Metal / material. `ENGRAVE`: Engraving pattern. `ENGRAVEM`: Engraving metal. `TINT`: Colour.
* A price is charged once per changed entry; the server computes the total from the stored components.

Every price can also pick its own currency, including items:

```lua
["SCOPE"] = {
    ["COMP"]     = {Type = "item",  Item = "scope_lens", Amount = 1, Label = "Scope Lens"},
    ["MATERIAL"] = {Type = "money", Amount = 10},
    ["ENGRAVE"]  = {Type = "gold",  Amount = 0.5},
    ["ENGRAVEM"] = 10, -- plain number = WeaponEditPayment.Type
},
```

* `Type`: `gold`, `money` or `item`. `Amount`: how much / how many. `Item` + `Label`: the inventory item and the name shown in the editor.
* Mixed costs add up per currency (for example `12 Gold · $30 · 1x Scope Lens`). The player must have all of it before anything is taken; the editor shows the cost on every card, in every options group and in the total.

***

## Poison & Tranquilizer

```lua
ActivePoison = false
PoisonOnPlayers = true
Poison = { WaitBeforeStart = {6, 22}, Duration = 120, Damage = 70, DamageEvery = {15, 40}, StaminaDecreaser = 1.5 }

ActiveTranq = false
TranqOnPlayers = false
Tranq = { WaitBeforeStart = {5, 15}, Duration = 60 }
```

Disabled by default. Hits are rate-limited and distance-checked on the server.

***

## Stores & Gunsmith Benches

```lua
Config.Stores = {
    [1] = {
        Name = "GunSmith",

        EnableStore = true,
        StoreBlip = 202506373,
        CatalogWeapon = {-281.4826, 780.6805, 119.4771, 187.0176},
        CamStore = {-281.23, 779.84, 120.00, -90.0, -180.0, 0.0, 50.0},
        WichWeapons = false,
        WichAmmo = false,
        Serial = true,
        CustomLabel = true,

        EnableGunsmith = true,
        GunSmithBlip = 1321928545,
        ModifyWeapons = {-277.2002, 778.7532, 119.4539},
        ModifyPos = {-276.20, 778.82, 119.55, 90.0, 180.0, -89.73},
        CamGunSmith = {-276.29, 778.99, 120.00, -90.0, 0.0, -90.0, 80.0},
        Jobs = {"Guvernator", "Manager", "ArmurierVAL", "Armurier"},
    },
}
```

* `EnableStore` / `EnableGunsmith`: Enable the catalogue and / or the bench.
* `WichWeapons` / `WichAmmo`: `false` = whole catalog, `{}` = nothing, list = only those keys.
* `Serial`: `true` = paid custom serial option, `false` = no option.
* `CustomLabel`: `true` = paid custom name option, `false` = no option, `"Text"` = every weapon sold here gets this name for free.
* `ModifyPos`: Where the preview weapon lies on the bench. `CamGunSmith`: Camera position, rotation and FOV (the defaults look straight down for the blueprint view).
* `Jobs`: Jobs allowed at the bench (`false` / `nil` = everyone). Checked again on the server.

***

## Weapon Catalog

```lua
["WEAPON_REVOLVER_CATTLEMAN"] = {
    Weapon = "WEAPON_REVOLVER_CATTLEMAN",
    Label = "Cattleman Revolver",
    Tittle = "Cattleman Revolver",
    Description = "The Cattleman Revolver is a dependable weapon...",
    Extra = "A classic ranch piece...",
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

`BuyJobs` / `BuyJobsGrade` limit who can buy, `ModifyJobs` / `ModifyJobsGrade` who can customize. Empty table = everyone.

***

## Ammo Catalog

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

* `Type`: Ammo type added to the belt. `MaxAmmo`: Belt limit. `Amount`: Bullets per box.

***

## config.js (UI)

```js
var Config = { Language: "EN" };

var UiConfig = {
    filterCategory: true, // category tabs in the catalogue
    storeThumbs: true,    // weapon thumbnails in the list
    calloutDots: true,    // brass ring where each line touches the weapon
    calloutCurve: true,   // elbow lines (false = straight)
};
```

The `Languages` table below it holds every UI text for the 8 languages.
