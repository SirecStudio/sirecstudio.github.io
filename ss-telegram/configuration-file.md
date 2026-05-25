---
description: Default SS-Telegram config file.
---

# Configuration File

```
-- Author: SIREC
-- Support / bug reports: https://discord.gg/9XNBaQSmMd
--
--[[
===========================================================================
 SS-Telegram Configuration
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

    Dev = true, -- true = extra logs/dev commands | false = recommended for live server

    -- Available languages already included in l/l.lua:
    -- EN / IT / ES / FR / DE / PT / RU / RO
    Language = "EN",

    Key = 0xD9D0E1C0, -- prompt key used to call/open/read/write telegrams

    AutoSetupDatabase = true, -- true = create required tables/columns automatically on resource start

    --=====================================================================
    -- OPTIONAL / ADDON INTEGRATIONS
    -- Enable only if those resources exist on your server
    --=====================================================================

    SSIdentityCard = true, -- true = use SS-IdentityCard names/data for recipients and sender identities

    -- Jobs listed here can send telegrams using the institution/job name.
    OfficialJobs = {"police", "SheriffValentine"},

    --=====================================================================
    -- DISCORD WEBHOOK SETTINGS
    --=====================================================================

    Webhook = "", -- webhook URL | leave empty to disable logs
    WebhookTittle = "NEW TELEGRAM HAS BEEN SENT", -- webhook title

    --=====================================================================
    -- TELEGRAM DATE / UI SETTINGS
    --=====================================================================

    CustomDate = "08/1875", -- custom month/year printed in sent telegram text | false = use game date

    --=====================================================================
    -- BIRD / CAMERA SETTINGS
    --=====================================================================

    Use3DCam = false, -- true = enables optional 3D camera prompt while calling the bird
    CameraKey = 0x4BC9DABB, -- key used to switch optional 3D camera

    Model = "A_C_Eagle_01", -- normal telegram bird model
    ModelAnonymouse = "a_c_crow_01", -- anonymous telegram bird model

    --=====================================================================
    -- MONEY / ITEM SETTINGS
    --=====================================================================

    EnableSendMoney = true, -- true = players can attach money to telegrams | false = disable money option completely
    EnableShareLocation = true, -- true = players can attach location/blip/GPS | false = disable location option completely

    MaxMoneyAmount = 500, -- maximum money amount that can be sent by telegram

    Telegram = "telegram", -- usable item used to send normal telegrams
    AnonymousTelegram = "blacktelegram", -- usable item used to send anonymous telegrams

    -- true = players can send unlimited telegrams while having the item
    -- false = one item is removed for each telegram sent
    UnlimitedTelegram = false,

    --=====================================================================
    -- TIMERS / FAILSAFE SETTINGS
    --=====================================================================

    TimeCheck = 60, -- seconds between checks for new telegrams
    ResetTelegram = 600, -- seconds before stuck/dead bird reset | false = disable reset
}

function NOTIFY(text)
    -- Default VORP notification. Replace this event if your server uses another notify system.
    TriggerEvent("vorp:TipBottom", text, 5000)
end

```
