# Configuration File

## config.lua

{% code overflow="wrap" %}
```lua
-- Author: SIREC
-- Support / bug reports: https://discord.gg/9XNBaQSmMd
--
--[[
===========================================================================
 SS-Archives Configuration
===========================================================================
 This file is written to be easy to understand even for server owners who
 do not work with Lua often.

 IMPORTANT RULES:
 1. Change values, not logic.
 2. Use Dev = true only while testing.
 3. If you do not use an optional integration, disable it here.
 4. Read README.md before changing offices, penitentiary settings, or jobs.
===========================================================================
]]

Config = {

    --=====================================================================
    -- GENERAL SETTINGS
    --=====================================================================

    Dev = true, -- true = extra console logs for testing | false = recommended for live server

    -- Available languages included in l/l.lua:
    -- EN / IT / ES / FR / DE / PT / RU / RO
    Language = "EN",

    SSHousing = true, -- true only if you use SS-Housing integration
    SSPlayerShops = true, -- true only if you use SS-PlayerShops integration
    WebHook = "", -- Discord webhook URL for archive action logs | leave empty to disable

    Align = "right", -- menu alignment used by menuapi
    Button = "PRESS", -- menu prompt button text
    Key = 0xD9D0E1C0, -- key used to open archive prompts
    ServerYear = "1905", -- world/server lore year shown on records

    -- Tax system.
    -- NOTE: TaxDays is currently disabled in runtime because jailtime is now
    -- used as online remaining jail time, not absolute timestamp.
    TaxDays = 10,
    TaxPercentual = 10,

    DrinkItem = "water", -- canteen drink item
    FoodItem = "bread", -- canteen food item

    BountyHunter = true, -- true if you use SS-BountyHunter integration
    PayFromSheriff = true, -- true = bounty money is taken from the sheriff officer

    AllowedJobs = {"Guvernator", "marshal", "sheriff", "police"}, -- jobs allowed to open and use the archive
    OfficerNotesCooldown = 1, -- minutes between officer notes | minimum is 1
    PropertyOnly = {"Primar"}, -- reserved list used by property-related logic
    DeleteNotesGrade = 5, -- minimum grade required to remove notes
    DeleteJobGrade = 9, -- minimum grade required to delete dossiers
    SeizureProperty = 5, -- minimum grade required to seize property/stores
    TransferProperty = 8, -- minimum grade required to transfer property/stores

    AutoEject = true, -- eject civilians who enter prison zone if not allowed
    AutoTeleport = true, -- teleport prisoners back if they escape prison range
    AutoDoors = true, -- old door flow placeholder, keep true only if you still need that legacy behavior

    NoteBook = "archivesbook", -- usable inventory item that opens the archive UI
    DossierItem = "sulf", -- usable item given as a dossier copy

    ShowJailDossier = "showdossier", -- command used to show jail paper while jailed
    HideJailDossier = "hidedossier", -- command used to hide jail paper while jailed
    TimeToCheckJail = 60000, -- milliseconds between jail checks
    AutoJail = true, -- true = officer can choose automatic jail when creating a dossier
    ShowJailInfo = true, -- true = jail paper can be shown while jailed

    --=====================================================================
    -- ARCHIVE OFFICES
    -- Pos format = {x, y, z, heading}
    -- Distance = interaction range
    -- Blip = blip hash | false = hide blip
    --=====================================================================

    Offices = {
        [1] = {
            Name = "Blackwater Archive",
            Pos = {-761.92901611328, -1266.8898925782, 44.050498962402, 170.40016174316},
            Blip = 587827268,
            Distance = 2.0,
        }
    },

    --=====================================================================
    -- PRISON CROP JOB
    -- WorkBonus = how many seconds are removed per completed crop
    -- Money = false disables payment, or set a number to reward prisoners
    --=====================================================================

    CropJob = {
        Name = "Work for the benefit of the Country",
        Angles = {
            vector2(3300.67, -593.41),
            vector2(3278.85, -596.57),
            vector2(3214.08, -554.26),
            vector2(3248.91, -501.93),
            vector2(3328.92, -552.39)
        },
        Zcoords = {35, 54},
        WorkBonus = 20,
        Money = false,
        Debug = false,
        ReWorkDistance = 8.0,
        WaitCrop = 10000,
    },

    -- Reserved for future jobs logic
    Jobs = {},

    --=====================================================================
    -- PENITENTIARY SETTINGS
    -- Cells = possible prison cell spawn points
    -- JailPos = manual jail delivery point
    -- SpawnBoat / BoatModel = manual jail transport sequence
    --=====================================================================

    Penintetiary = {
        Name = "Sisika Penitetiary",
        Angles = {
            vector2(3386.60, -636.57),
            vector2(3410.79, -678.88),
            vector2(3369.20, -727.20),
            vector2(3329.68, -703.74),
            vector2(3315.48, -655.87)
        },
        Zcoords = {42, 54},
        Debug = true,
        Blip = -1489164512,
        Pos = {3363.4689941406, -681.2964477539, 46.466829681396},
        Canteen = {3334.93603515625, -658.6146850585938, 45.97416305541992, 281.05603027344},
        CanteenName = "Sisika Canteen",
        CanteenBlip = -1138864184,
        CanteenDistance = 2.0,
        Cells = {
            [1] = {3328.6863, -668.3199, 48.8897, 27.1767},
            [2] = {3327.9915, -661.4512, 48.8881, 89.6623},
            [3] = {3332.6626, -667.0618, 48.8896, 197.2037},
            [4] = {3333.2444, -659.8171, 48.8896, 26.3801},
            [5] = {3336.9790, -666.5901, 48.8897, 181.3364},
            [6] = {3337.1565, -658.8512, 48.8917, 12.6926},
            [7] = {3341.1169, -665.6801, 48.8897, 278.9239},
            [8] = {3341.5369, -657.7955, 48.8924, 7.8863}
        },
        JobPermit = {3380.7498, -659.0895, 46.9061, 28.9527, 45.64087295532226},
        JobPermitName = "Job Permission",
        JobPermitBlip = 1109348405,
        ReleasePos = {2685.7255859375, -1454.185913086, 46.278060913086, 187.82933044434},
        Range = 100,
        NpcMenuModel = "s_m_m_ambientblwpolice_01",
        NpcMenu = {3353.7534179688, -641.92889404296, 44.29126739502, 13.36182308197},
        JailPos = {2926.742919921875, -1254.27099609375, 42.38059997558594},
        JailDistance = 10.0,
        SpawnBoat = {2949.8779296875, -1246.3270263671875, 40.50966644287109, -82.29},
        BoatModel = "rowboat",
        NpcGuardModel = "s_m_m_skpguard_01",
        NpcGuard = {3347.1630859375, -643.75970458984, 44.291255950928, 23.405473709106},
    },
}

function ARCHIVESNOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000)
end

function ADDFINES(source, charid, amount, tittle, description)
    TriggerEvent("S!r@#Blu$$-SS-ARCHIVES:SERVER:SENDFINE", source, charid, amount)
end
```
{% endcode %}

