---
description: Configuration and Usage Guide for the SS-Crafting Script in RedM
---

# Configuration File

The configuration file defines settings for crafting items in the game, including crafting books, recipes, and other parameters such as language, keys, explosion effects, and permanent items.

{% code overflow="wrap" %}
```lua
-- Author 'SIREC' Discord Username
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd --

Config = {
    Dev = true,  -- USE ONLY ON TEST SERVER FOR CONFIGURATION & TESTS
    Language = "EN", -- TRANSLATE LANGUAGE ("EN")
    Key = 0xD9D0E1C0, -- KEY TO OPEN MENU/PARK
    
    ExplodeFailCraft = 35, -- EXPLOSION TYPE 35 = POISON, 32 = FIRE EFFECT, 24 = FIRE EXPLOSION, 3 = LOW EXPLOSION / false TO TURN IT OFF
    ExplosionPower = 0.7, -- 0.0 - 1.0 / TEST AND CHOOSE
    
    PermanentItems = { -- ITEMS THAT JUST NEED TO BE IN INVENTORY, WILL NOT BE REMOVED WHEN CRAFTING
        ["hammer"] = true,
        ["shovel"] = true,
    }, 
    
    CraftBooks = {
        ["medicinebook"] = {
            Cover = "coverbook", -- IMAGE NAME (THE IMAGE MUST BE .png IN UI/img/*.png / FOLLOW THE DIMENSIONS OF THE EXAMPLE COVER)
            PropSpawn = "p_campfire_coloursmoke01x", -- SPAWN PROP FOR THIS BOOK ? false TO DISABLE
            Animation = {"amb_camp@world_camp_fire_tend_sit@poke_fire@male_a@base", "base"}, -- USE ANIMATION ? IF YES WHICH ? {dict, anim} false TO DISABLE
            Recipes = {"cigarette"},
        },
        ["jewelrybook"] = {
            Cover = "coverbook", -- IMAGE NAME
            PropSpawn = "p_campfire_coloursmoke01x", -- SPAWN PROP
            Animation = {"amb_camp@world_camp_fire_tend_sit@poke_fire@male_a@base", "base"}, -- USE ANIMATION
            Recipes = {"boiledegg", "porkcooked", "friedchicken", "scrambledeggsbacon", "fishchips", "pocket_watch", "WEAPON_MELEE_LANTERN", "WEAPON_MELEE_DAVY_LANTERN", "barrel"},
        },
        ["book"] = {
            Cover = "coverbook", -- IMAGE NAME
            PropSpawn = "p_campfire_coloursmoke01x", -- SPAWN PROP
            Animation = {"amb_camp@world_camp_fire_tend_sit@poke_fire@male_a@base", "base"}, -- USE ANIMATION
            Recipes = {"horsebrush"},
        },
    },
    
    Crafting = {
        ["cigarette"] = {
            Item = "cigarette", -- ITEM TO RECEIVE
            Amount = 1, -- AMOUNT TO RECEIVE WHEN CRAFTED
            Desc = "A handmade cigarette.", -- ITEM DESCRIPTION
            Category = "medicine", -- CATEGORY FOR EXPERIENCE
            Level = 0, -- LEVEL REQUIRED TO CRAFT
            Exp = 2, -- EXPERIENCE GAINED WHEN CRAFTED
            isGun = false, -- IS THIS ITEM A GUN?
            Jobs = {}, -- ALLOWED JOBS, EMPTY ARRAY FOR ALL JOBS
            JobGrades = {}, -- ALLOWED JOB GRADES
            SuccessRate = 90, -- % CHANCE TO SUCCESSFULLY CRAFT
            Time = 2, -- TIME REQUIRED TO CRAFT
            Metadata = false, -- ADD METADATA IF NEEDED
            Ingredients = { -- REQUIRED INGREDIENTS
                ['rollingpaper'] = {amount = 1, returnItem = false},
                ['tobacco'] = {amount = 2, returnItem = false},
            }
        },
        -- ADD MORE RECIPES HERE
    }
}

function NOTIFY(text) -- SET YOUR NOTIFICATIONS
    TriggerEvent("vorp:TipBottom", text, 5000)      
end

function playAnim(dict, name)
    local playerPed = PlayerPedId()
    RequestAnimDict(dict)
    while not HasAnimDictLoaded(dict) do
        Citizen.Wait(100)
    end
    TaskPlayAnim(playerPed, dict, name, 1.0, 1.0, -1, 1, 0, false, false, false)  
end

```
{% endcode %}

#### Using the Script

1. **Development Mode**: Set `Dev` to `true` for testing and configuration on a test server. Set it to `false` for production.
2. **Language**: Configure the language setting with `Language`.
3. **Key Bindings**: Define the key binding for opening the crafting menu with `Key`.
4. **Explosion Effects**: Configure the explosion effects for failed crafts using `ExplodeFailCraft` and `ExplosionPower`.
5. **Permanent Items**: List items in `PermanentItems` that will not be consumed during crafting.
6. **Crafting Books**: Define crafting books in `CraftBooks` with associated animations, props, and recipes.
7. **Crafting Recipes**: Configure recipes in the `Crafting` section, specifying items required, success rate, experience gained, and other parameters.

#### Final Considerations

This guide covers the basic configuration and use of the SS-Crafting script for RedM. You can further expand the functionality by adding new recipes, crafting books, and customizing the crafting experience based on your needs. If you have any further questions or need assistance, feel free to ask!
