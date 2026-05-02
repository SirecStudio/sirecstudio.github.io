# Configuration File

## config.lua

{% code overflow="wrap" %}
```lua
-- Author: SIREC
-- Support / bug reports: https://discord.gg/9XNBaQSmMd
--
--[[
===========================================================================
 SS-CommunityJobs Configuration
===========================================================================
 This file is written to be easy to understand even for people who do not
 work with Lua regularly.

 IMPORTANT RULES:
 1. Change values, not logic.
 2. If a feature depends on another script, disable it here when you do not
    have that resource on your server.
 3. Read README.md before changing integrations or adding new offices.
===========================================================================
]]

Config = {

    --=====================================================================
    -- GENERAL SETTINGS
    --=====================================================================

    -- AVAILABLE: EN / RO / IT / DE / FR / ES / PT
    Language = "EN", -- language used for all translated notifications and prompts

    SSMenu = false, -- true = use SS-Menu | false = use vorp_menu / menuapi
    Align = "right", -- menu alignment used by both supported menu systems

    --=====================================================================
    -- KEY SETTINGS
    --=====================================================================

    WorkButton = 0x8AAA0AD4, -- prompt key used to interact with the current work point
    StopButton = 0x760A9C6F, -- prompt key used to stop the active work session

    -- Legacy compatibility variables kept from the original script.
    -- They are not part of the active community jobs flow right now.
    EnterExitPassenger = 0x760A9C6F,
    RentBallon = 0x8AAA0AD4,
    BallonRoutes = 0x760A9C6F,

    --=====================================================================
    -- OPTIONAL / ADDON INTEGRATIONS
    -- Enable only if those resources exist on your server
    --=====================================================================

    SSIdentityCard = true, -- intended integration with SS-IdentityCard office flow
    SSArchives = true, -- enables forced labor and fine reduction integration
    DecreaseFines = true, -- true = withdrawn salary reduces fines first, then pays the remaining cash

    --=====================================================================
    -- BLIP / GPS SETTINGS
    --=====================================================================

    BlipStyle = "BLIP_STYLE_DEBUG_GREEN", -- style applied to generated job blips
    BlipGps = "COLOR_GREEN", -- GPS route color used for job destinations

    --=====================================================================
    -- COMMUNITY JOB OFFICES
    -- City key must match the external city that opens this menu.
    --
    -- OFFICE FIELDS:
    -- Name = office title in menu
    -- Description = office subtitle in menu
    -- Distance = prompt interaction distance
    --
    -- JOB FIELDS:
    -- Blip = blip sprite hash
    -- WorkTime = progress bar time in milliseconds
    -- Pay = random pay range {min, max}
    -- ForcedWork = true = reduces SS-Archives work tasks first
    -- WorkTitle = menu label
    -- WorkDesc = menu description
    -- Locations = work destinations
    -- Start = only used by CARRY as pickup location
    -- Prop = only used by CARRY as carried object model
    --=====================================================================

    Offices = {
        ["Annesburg"] = {
            Name = "Community Jobs",
            Description = "Work & Get Paid",
            Distance = 3.0,

            ["BROOM"] = {
                Blip = -576151168,
                WorkTime = 20000,
                Pay = {0.1, 0.9},
                ForcedWork = true,
                WorkTitle = "Broom The City",
                WorkDesc = "Broom & clean the city.",
                Locations = {
                    {2938.399169921875, 1308.7247314453125, 43.57914352416992},
                    {2957.786865234375, 1301.2540283203125, 43.5886116027832},
                    {2911.4111328125, 1307.12451171875, 43.77418899536133},
                    {2916.231689453125, 1319.9664306640625, 43.61255645751953},
                },
            },

            ["WINDOWS"] = {
                Blip = 1321928545,
                WorkTime = 20000,
                Pay = {0.1, 0.9},
                ForcedWork = true,
                WorkTitle = "Clean City Windows",
                WorkDesc = "Clean the city windows.",
                Locations = {
                    {2931.623291015625, 1291.8941650390625, 44.76031112670898},
                    {2928.22998046875, 1285.9609375, 44.7767219543457},
                    {2927.299072265625, 1283.5289306640625, 44.76520156860351},
                    {2926.19091796875, 1277.10888671875, 44.72944259643555},
                    {2931.369873046875, 1267.0167236328125, 44.75484848022461},
                    {2939.483154296875, 1279.17138671875, 44.73685455322265},
                    {2939.985595703125, 1280.4405517578125, 44.73633575439453},
                    {2940.375732421875, 1281.516357421875, 44.73600769042969},
                    {2941.58447265625, 1288.06640625, 44.73311996459961},
                    {2942.590576171875, 1290.5225830078125, 44.81488418579101},
                    {2935.00439453125, 1294.5941162109375, 44.7454719543457},
                },
            },

            ["CARRY"] = {
                Blip = 1321928545,
                WorkTime = 20000,
                Pay = {0.4, 1.2},
                ForcedWork = true,
                Prop = "p_woodpile06x",
                WorkTitle = "Carry Firewoods",
                WorkDesc = "Carry firewoods to the houses.",
                Start = {2905.87939453125, 1292.447509765625, 44.03779602050781},
                Locations = {
                    {2967.615966796875, 1422.7041015625, 44.64105224609375},
                    {2966.428955078125, 1437.837646484375, 45.17163467407226},
                    {2851.25537109375, 1447.829345703125, 67.52664947509766},
                    {2917.459228515625, 1355.168212890625, 43.5555191040039},
                    {2953.803955078125, 1326.9671630859375, 43.2729377746582},
                },
            },
        },
    },
}

function NOTIFY(text)
    exports["MNotify"]:Notify({
        image = "maiorca.png",
        title = TR["notify_title"],
        text = text,
        duration = 5000,
        position = "center-right"
    })
end
```
{% endcode %}

