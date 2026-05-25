---
description: Default Configuration File config.lua
---

# Configuration File

{% code overflow="wrap" %}
```lua
-- Author: SIREC
-- Support / bug reports: https://discord.gg/9XNBaQSmMd
--
--[[
===========================================================================
 SS-IdentityCard Configuration
===========================================================================
 This file is written to be easy to understand even for people who do not
 work with Lua regularly.

 IMPORTANT RULES:
 1. Change values, not logic.
 2. Use Dev = true only while testing.
 3. If a feature depends on another script, disable it here when you do not
    have that resource on your server.
 4. Read README.md before changing any integrations.
===========================================================================
]]

Config = {

    --=====================================================================
    -- GENERAL SETTINGS
    --=====================================================================

    Dev = false, -- true = extra logs/dev info | false = recommended for live server

    -- Available languages already included in l/l.lua:
    -- EN / IT / ES / FR / DE / PT / RU / RO
    Language = "EN",

    Key = 0xD9D0E1C0, -- key used to open the office menu
    Align = "right", -- menu alignment

    NXTInventory = false, -- true only if your server uses NXTInventory integration
    ServerName = "Sirec Studio", -- shown as the authority/sign under the ID photo

    -- Discord webhook settings
    WebHook = "", -- webhook URL | leave empty to disable
    WebHookInfo = "HAS REGISTERED HIS IDENTITY CARD ID WITH NR",
    WebHookUpdate = "HAS UPDATED HIS IDENTITY CARD",

    --=====================================================================
    -- OPTIONAL / ADDON INTEGRATIONS
    -- Enable only if those resources exist on your server
    --=====================================================================

    ImigrationStamp = "stampilabilet", -- usable item used for immigration stamp in/out
    SSMedicArchives = true,
    SSArchives = true, -- enables fines/payment integration
    SSLicenses = true, -- enables licenses menu
    SSHousing = true, -- enables house certificate menu
    SSPlayerShops = true, -- enables shop certificate menu
    SSBoats = true, -- enables boat certificate menu
    SSTrainTransport = true, -- enables train ticket button/event
    SSPrimary = true, -- enables jobs panel button/event
    SSCommunityJobs = true, -- enables community jobs button/event

    --=====================================================================
    -- REAL IDENTITY CARD SETTINGS
    --=====================================================================

    IdentityCardItem = "identitycard", -- usable inventory item for the real ID card
    PayRegistration = 5, -- false = free | number = registration price
    PayCopyRegistration = 1, -- false = free copy | number = copy price
    PayInfoUpdate = 1, -- false = free update | number = update price
    AllowImageInGame = true, -- true = players can add/update image URL from UI

    --=====================================================================
    -- FAKE IDENTITY CARD SETTINGS
    --=====================================================================

    FakeIdentityCardItem = "salt", -- usable inventory item for the fake ID card
    PayFakeId = 250, -- false = disable fake registration price | number = price
    PayFakeCopyId = 150, -- false = free fake copy | number = fake copy price
    Only1FakeId = false, -- true = player can only ever keep one fake ID at a time
    PayDeleteFakeId = 1000, -- false = free delete | number = delete fake ID price

    --=====================================================================
    -- JOB / PRIVACY / MONEY SETTINGS
    --=====================================================================

    SynSociety = "police", -- job account that receives fine money | false = disable
    SSBank = false, -- bank integration placeholder, keep false unless you support it

    -- Jobs listed here will not be shown on the visible ID card.
    BlackListJobs = {"police", "marshal"},
    ReplaceBlackListJobs = "Unemployed", -- replacement text shown instead of blacklisted job
    FakeIdDefaultJob = "Unemployed", -- job text always shown on fake identity cards

    -- Which jobs are allowed to inspect / stamp / work with identity card data.
    -- false = everyone can interact with this part of the script
    PoliceJobs = false, -- example: {"police", "marshall"}

    --=====================================================================
    -- AGE / SERVER LORE SETTINGS
    --=====================================================================

    ServerYear = 1905, -- year printed on registrations and used to validate age
    MaxYears = 80, -- maximum player age allowed on registration
    MinYears = 18, -- minimum player age allowed on registration

    --=====================================================================
    -- VISUAL / ANIMATION SETTINGS
    --=====================================================================

    UseAnimProp = true, -- true = show card prop + animation while presenting the ID

    --=====================================================================
    -- NATIONAL REGISTRATION OFFICES
    -- Each office creates an NPC and optional blip.
    -- FakeServices = true means this office opens the fake ID menu.
    -- Pos format = {x, y, z, heading}
    --=====================================================================

    NationalRegistration = {
        [1] = {
            City = "Valentine", -- city printed on IDs registered here
            FakeServices = false, -- false = real ID office | true = fake ID office
            Name = "Valentine NR Office", -- menu/blip title
            Desc = "NATIONAL OFFICE", -- menu subtitle/description
            NpcModel = "S_M_M_VHTDEALER_01", -- NPC model
            Pos = {-175.2606048584, 631.74407958984, 113.08966064454, 320.85287475586},
            Distance = 3.0, -- interaction distance
            Blip = 587827268, -- blip hash | false = hide blip
        },
        [2] = {
            City = "Blackwater",
            FakeServices = false,
            Name = "BlackWater NR Office",
            Desc = "NATIONAL OFFICE",
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {-762.0810546875, -1272.1394042968, 43.050540924072, 86.552299499512},
            Distance = 3.0,
            Blip = 587827268,
        },
        [3] = {
            City = "Rhodes",
            FakeServices = false,
            Name = "Rhodes NR Office",
            Desc = "NATIONAL OFFICE",
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {1230.1987304688, -1298.5638427734, 75.904258728028, 232.19049072266},
            Distance = 3.0,
            Blip = 587827268,
        },
        [4] = {
            City = "Saint Denis",
            FakeServices = false,
            Name = "Saint Denis NR Office",
            Desc = "NATIONAL OFFICE",
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {2747.9025878906, -1396.4379882812, 46.183067321778, 24.291278839112},
            Distance = 3.0,
            Blip = 587827268,
        },
        [5] = {
            City = "Saint Denis",
            FakeServices = true,
            Name = "Mrs Thomson",
            Desc = "NATIONAL OFFICE",
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {2859.19140625, -1202.2645263672, 48.590869903564, 1.381891965866},
            Distance = 3.0,
            Blip = false,
        },
        [6] = {
            City = "Annesburg",
            FakeServices = false,
            Name = "Oficiul Postal Annesburg",
            Desc = "Oficiu Postal",             
            NpcModel = "s_m_m_nbxriverboatguards_01",
            Pos = {2938.853759765625, 1286.9677734375, 43.75288391113281, -22.61572074890136},
            Distance = 3.0,
            Blip = -1656531561,
        },
    },
}

function NOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000)
end

--[[
===========================================================================
EXPORTS / CALLBACK USAGE
===========================================================================

1) exports["SS-IdentityCard"]:GetIdentityCard()
   Returns your loaded real identity card table or false.

2) exports["SS-IdentityCard"]:GetIdentityFakeCard()
   Returns your loaded fake identity card table or false.

3) exports["SS-IdentityCard"]:GetIdCard(recordid)
   Returns a specific identity card from the server by record ID.

4) SSCORE.TriggerServerCallback("SS-IDENTITYCARD:SERVER:GETDATA", function(allIds)
   Returns all identity cards.
end)

5) SSCORE.TriggerServerCallback("S!r@#Blu$$-SS-ARCHIVES:SERVER:GETIDCARD", function(idCard)
   Returns one specific identity card by ID number / record ID.
end, idcard)

REGISTER THROUGH TRIGGER WITH THESE FIELDS:
local info = {
    year = "1855",
    eyes = "blue",
    recordid = "K54V86Y73",
    sex = "M",
    city = "Saint Denis",
    firstname = "Fane",
    lastname = "Baboia",
    kg = "80",
    date = "04-11-1905",
    month = "12",
    dob = "1855-12-11",
    cm = "180",
    hair = "black",
    day = "11"
}
TriggerServerEvent("S!r@#Blu$$-SS-IDENTITYCARD:SERVER:REGISTERID", info)
]]

```
{% endcode %}

