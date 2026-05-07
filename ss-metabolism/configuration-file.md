# Configuration File

## config.lua

{% code overflow="wrap" %}
```lua
-- Author: SIREC
-- Support / bug reports: https://discord.gg/9XNBaQSmMd
--
--[[
===========================================================================
 SS-Metabolism Configuration
===========================================================================
 This file is written to be easy to understand even for people who do not
 work with Lua regularly.

 IMPORTANT RULES:
 1. Change values, not logic.
 2. Use Dev = true only while testing.
 3. If a feature depends on another script, disable it here when you do not
    have that resource on your server.
 4. Read README.md before changing UI, metabolism, horse, housing or item
    settings.
===========================================================================
]]

Config = {

    --=====================================================================
    -- GENERAL SETTINGS
    --=====================================================================

    Dev = true, -- true = dev/test mode | false = recommended for live server
    WaitBeforeLoad = 10, -- seconds to wait after character selected before HUD loads

    CommandSetHud = "sethud", -- opens HUD edit mode: move icons, scale, hide/show, save with ESC
    ToggleHud = "shud", -- show/hide the full HUD

    -- Main metabolism tick.
    -- This updates hungry, thirsty, stress, dirtiness, reputation and horse metabolism.
    -- Health/stamina cores are refreshed separately and faster.
    Refresh = 20, -- seconds | recommended 10-20+

    -- Database save throttle for player metabolism info.
    -- HUD can refresh more often, but DB saves are limited by this value.
    SaveRefresh = 60, -- seconds

    -- Clock style shown in the HUD.
    -- Options: "analog" or "digital"
    ClockMode = "analog",

    --=====================================================================
    -- INITIAL PLAYER VALUES
    -- Used when the character has no saved metabolism data yet.
    -- Values are percentages, except Reputation which is 0-1000 internally.
    --=====================================================================

    Initial = {
        Thirsty = 90,
        Hungry = 75,
        Stress = 10,
        Reputation = 100,
    },

    --=====================================================================
    -- HUD FEATURE SWITCHES
    --=====================================================================

    UseHealthStamina = true, -- true = custom player health/stamina cores
    UseHorseHealthStamina = true, -- true = custom horse health/stamina cores
    HorseStats = true, -- true = horse hungry/thirsty HUD and decrease system
    RepStats = true, -- true = reputation HUD and NPC reaction system

    --=====================================================================
    -- HOUSING HUD INTEGRATION
    -- This script does not own housing logic. External scripts can use:
    -- exports["SS-Metabolism"]:SetHousing(mode, number)
    -- exports["SS-Metabolism"]:HousingIcon(icon)
    --=====================================================================

    SSHousing = true,
    HouseIcons = {
        ["stash"] = "housingkey_bg.png",
        ["outfit"] = "housingkey_bg.png",
        ["crafting"] = "housingkey_bg.png",
        ["phone"] = "housingkey_bg.png",
    },

    --=====================================================================
    -- REPUTATION / NPC REACTION SETTINGS
    -- Reputation is stored internally from 0 to 1000.
    -- GetRep() export returns floor(REP / 100), so 0-10.
    --=====================================================================

    ActiveNpcHate = true, -- true = NPCs can react to very low reputation
    RadiusNpc = 20.0, -- radius used to search nearby NPCs
    PeopleStartWalkingAway = 3, -- NPCs walk away when reputation level is this low
    PeopleStartRunningAway = 2, -- NPCs run away when reputation level is this low
    PeopleStartHateYou = 1, -- NPCs may fight/shoot when reputation level is this low

    -- Models listed here are ignored by the reputation reaction system.
    BlackListModels = {
        "a_m_m_valtownfolk_01",
        "mp_u_m_m_lom_train_prisoners_01",
        "g_m_m_bountyhunters_01",
        "g_m_m_unibanditos_01",
        "re_street_fight_males_01",
        "U_M_M_BHT_ODRISCOLLSLEEPING",
        "re_street_fight_males_01",
        "mp_g_m_m_bountyhunters_01",
        "U_M_M_BHT_ODRISCOLLMAULED",
        "U_M_M_BHT_ODRISCOLLDRUNK",
    },

    --=====================================================================
    -- HORSE METABOLISM SETTINGS
    -- These values are removed every Config.Refresh tick while the player
    -- has a horse loaded and HorseStats is enabled.
    --=====================================================================

    HorseMetabolism = {
        Thirsty = 1,
        Hungry = 1,
    },

    --=====================================================================
    -- TEMPERATURE SETTINGS
    -- Temperature = {min, max}
    -- Clothing entries add warmth to the current external temperature.
    -- MIN/MAX entries define metabolism changes when the final temperature
    -- is outside the safe range.
    --=====================================================================

    Temperature = {3, 35},
    TemperatureSettings = {
        ["HAT"] = 1,
        ["SHIRT"] = 2,
        ["PANTS"] = 3,
        ["BOOTS"] = 2,
        ["COAT"] = 5,
        ["GLOVES"] = 2,
        ["VEST"] = 2,
        ["PONCHO"] = 5,
        ["MIN"] = {Thirsty = 0, Hungry = 0.5, Stress = 0.2},
        ["MAX"] = {Thirsty = 0.5, Hungry = 0, Stress = 0.2},
    },

    --=====================================================================
    -- METABOLISM DECREASE SETTINGS
    -- Hungry/Thirsty values are removed.
    -- Stress values are added. Negative stress means stress goes down.
    --=====================================================================

    Metabolism = {
        ["Idle"] = {Thirsty = 0.4, Hungry = 0.3, Stress = 0},
        ["Walking"] = {Thirsty = 0.7, Hungry = 0.6, Stress = 0},
        ["Running"] = {Thirsty = 1.0, Hungry = 0.8, Stress = 0},
        ["Combat"] = {Thirsty = 1.2, Hungry = 1.2, Stress = 5},
        ["InBoat"] = {Thirsty = 0.5, Hungry = 0.4, Stress = -5},
        ["InWagon"] = {Thirsty = 0.5, Hungry = 0.4, Stress = -3},
        ["OnMount"] = {Thirsty = 0.4, Hungry = 0.4, Stress = -1},
    },

    KillWhenZero = false, -- true = kill/reset player when hungry or thirsty reaches 0
    DecreaseByStress = 0.2, -- extra hungry/thirsty decrease based on stress percent

    -- What happens when hungry/thirsty goes below MetabolismMin.
    MetabolismMin = 20,
    MetabolismStats = {
        ["THIRSTY"] = {Health = 30, Stamina = 10, Stress = 5},
        ["HUNGRY"] = {Health = 25, Stamina = 5, Stress = 5},
    },

    --=====================================================================
    -- STRESS EFFECT SETTINGS
    --=====================================================================

    StressRagdoll = true,
    RagDollObjects = true, -- true = player can ragdoll when sprinting into objects
    RagDollObjectsChance = 85,
    RagDollFalling = false, -- true = high falls can trigger ragdoll task

    -- Stamina drains faster when stress is high.
    DecreaseFasterStamina1 = 1.5, -- used at stress >= 50
    DecreaseFasterStamina2 = 2.0, -- used at stress >= 80
    StressChance1 = 50, -- chance gate for stress >= 50
    StressChance2 = 50, -- chance gate for stress >= 80

    --=====================================================================
    -- USABLE GOODS / ITEMS
    -- Each entry registers one usable item through SS-Core.
    --
    -- Supported Mode values:
    -- EAT / DRINK / SMOKE / SYRINGE / BOWL / BOTTLE / BANDAGE
    --
    -- Metabolism fields:
    -- hunger  = adds hungry value
    -- thirsty = adds thirst value
    -- stress  = adds stress value; negative removes stress
    -- health  = heals player by value, or false
    -- stamina = restores stamina by value, or false
    --
    -- false means disabled for that field.
    --
    -- Example:
    -- ["apple"] = {
    --     Label = "Apple",
    --     Mode = "EAT",
    --     Prop = "p_apple01x",
    --     Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
    --     Times = 1,
    --     Alcohol = false,
    --     Effect = false,
    --     OverPowerStamina = false,
    --     OverPowerHealth = false,
    -- },
    --=====================================================================

    Goods = {
	-- FOOD
	["apple"] = {
		Label = "Mar",
        Mode = "EAT", -- EAT / DRINK / SMOKE / SYRINGE / BOWL / BOTTLE
        Prop = "p_apple01x", -- THE PROP TO USE / false DISABLE
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false}, -- CHOICE WHAT DO    
		Times = 1, -- HOW MANY TIME DRINK/EAT TO FINISH !
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false,
        OverPowerHealth = false,    
	},
	["bread"] = {
		Label = "Paine",
        Mode = "EAT",
        Prop = "p_bread_13_ab_s_a",
        Metabolism = {hunger = 30, thirsty = false, stress = -3, health = false, stamina = false},  
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_pear"] = {
		Label = "Para",
        Mode = "EAT",
        Prop = "p_pear_02x",
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_peach"] = {
		Label = "Piersica",
        Mode = "EAT",
        Prop = "s_peach01x",
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
    ["Red_Raspberry"] = {
		Label = "Zmeura",
        Mode = "EAT",
        Prop = "p_blackberry01x",
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
    ["Black_Berry"] = {
		Label = "Mure",
        Mode = "EAT",
        Prop = "p_blackberry01x",
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
    ["grapes"] = {
		Label = "Struguri",
        Mode = "EAT",
        Prop = "p_blackberry01x",
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
    ["Creekplum"] = {
		Label = "Prune",
        Mode = "EAT",
        Prop = "p_blackberry01x",
        Metabolism = {hunger = 20, thirsty = 10, stress = -2, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["boiledegg"] = {
		Label = "Ou Fiert",
        Mode = "EAT",
        Prop = "p_egg01x",
        Metabolism = {hunger = 10, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["consumable_salmon"] = {
		Label = "Somon",
        Mode = "EAT",
        Prop = "p_whitefishfilet01xb",
        Metabolism = {hunger = 30, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false, 
	},
	["consumable_trout"] = {
		Label = "Pastrav Prajit",
        Mode = "EAT",
        Prop = "p_whitefishfilet01xb",
        Metabolism = {hunger = 30, thirsty = false, stress = -5, health = false, stamina = false}, 
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["consumable_salmon_can"] = {
		Label = "Somon la conserva",
        Mode = "EAT",
        Prop = "s_canBeans01x",
        Metabolism = {hunger = 40, thirsty = 10, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["consumable_bluegil"] = {
		Label = "Platica gatita",
        Mode = "EAT",
        Prop = "p_cs_meatstewsmall01x",
        Metabolism = {hunger = 30, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["consumable_game"] = {
		Label = "Carne de vanat",
        Mode = "EAT",
        Prop = "p_cs_duckmeat01x",
        Metabolism = {hunger = 50, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["beefjerky"] = {
		Label = "Pastrama de vita",
        Mode = "EAT",
        Prop = "p_wrappedmeat01x",
        Metabolism = {hunger = 60, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,
	},
	["consumable_kidneybeans_can"] = {
		Label = "Fasole la conserva",
        Mode = "EAT",
        Prop = "s_canbeansused01x",
        Metabolism = {hunger = 30, thirsty = 30, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_chocolate"] = {
		Label = "Ciocolata",
        Mode = "EAT",
        Prop = "s_chocolatebar02x",
        Metabolism = {hunger = 25, thirsty = false, stress = -5, health = false, stamina = 50},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_caramel"] = {
		Label = "Caramel",
        Mode = "EAT",
        Prop = "s_chocolatebar02x",
        Metabolism = {hunger = 5, thirsty = 1, stress = -5, health = false, stamina = 10},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = 1.0, 
        OverPowerHealth = false,    
	},
	["caviar"] = {
		Label = "Icre Negre",
        Mode = "EAT",
        Prop = "s_canbeansused01x",
        Metabolism = {hunger = 25, thirsty = 25, stress = -5, health = false, stamina = 10},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["roe"] = {
		Label = "Icre la conserva",
        Mode = "EAT",
        Prop = "s_canbeansused01x",
        Metabolism = {hunger = 40, thirsty = 1, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["fishchips"] = {
		Label = "Peste cu cartofi",
        Mode = "EAT",
        Prop = "p_redfishfilet01xa",
        Metabolism = {hunger = 60, thirsty = 1, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["porkbacon"] = {
		Label = "Bacon",
        Mode = "EAT",
        Prop = "p_bacon_cabbage01x",
        Metabolism = {hunger = 30, thirsty = 1, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["fishcookedlmb"] = {
		Label = "Biban Prajit",
        Mode = "EAT",
        Prop = "p_main_friedcatfish02x",
        Metabolism = {hunger = 40, thirsty = 1, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["birdmeatcook"] = {
		Label = "Carne de pasare gatita",
        Mode = "EAT",
        Prop = "p_cs_rabbitmeat02x",
        Metabolism = {hunger = 50, thirsty = 1, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["friedchicken"] = {
		Label = "Pui prajit",
        Mode = "EAT",
        Prop = "p_main_prairiechicken01x",
        Metabolism = {hunger = 50, thirsty = 1, stress = -5, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["steakveg"] = {
		Label = "Friptura cu legume",
        Mode = "BOWL",
        Prop = "p_stewplate01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_breakfast"] = {
		Label = "Mic Dejun",
        Mode = "BOWL",
        Prop = "p_cs_platestew01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false, --
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_meat_greavy"] = {
		Label = "Sos cu carne",
        Mode = "BOWL",
        Prop = "p_camp_plate_02x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["spaghetti"] = {
		Label = "Spaghete cu chiftele",
        Mode = "BOWL",
        Prop = "p_camp_plate_01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["porkcooked"] = {
		Label = "Carne de porc gatita",
        Mode = "BOWL",
        Prop = "p_stewplate01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["steakpierce"] = {
		Label = "Platou cu friptura",
        Mode = "BOWL",
        Prop = "p_crab_plate_02",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["muttoncooked"] = {
		Label = "Carne de oaie gatita",
        Mode = "BOWL",
        Prop = "p_camp_plate_02x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["deckersroast"] = {
		Label = "Tocanita cu carne",
        Mode = "BOWL",
        Prop = "p_stewplate01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["primerib"] = {
		Label = "Costita cu legume",
        Mode = "BOWL",
        Prop = "p_cs_platestew01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["biggamecooked"] = {
		Label = "Cotlete carne vanat",
        Mode = "BOWL",
        Prop = "p_camp_plate_01x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["scrambledeggsbacon"] = {
		Label = "Omleta cu bacon",
        Mode = "BOWL",
        Prop = "p_bowl03x",
        Metabolism = {hunger = 20, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_veggies"] = {
		Label = "Legume comestibile",
        Mode = "BOWL",
        Prop = "mp006_p_bowl_apple01x",
        Metabolism = {hunger = 20, thirsty = 15, stress = -5, health = false, stamina = false},
		Times = 3,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["consumable_fruitsalad"] = {
		Label = "Salata de fructe",
        Mode = "BOWL",
        Prop = "mp006_p_bowl_banana01x",
        Metabolism = {hunger = 15, thirsty = 15, stress = -5, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["vanillacake"] = {
		Label = "Prajitura vanilie",
        Mode = "BOWL",
        Prop = "mp006_p_bowl_banana01x",
        Metabolism = {hunger = 25, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 4,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["chococake"] = {
		Label = "Prajitura ciocolata",
        Mode = "BOWL",
        Prop = "mp006_p_bowl_banana01x",
        Metabolism = {hunger = 25, thirsty = false, stress = -5, health = false, stamina = false},
		Times = 4,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	-- DRINKS !
	["water"] = {
		Label = "Apa",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer01a",
        Metabolism = {hunger = false, thirsty = 30, stress = -2, health = false, stamina = false},
		Times = 2,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false,
        OverPowerHealth = false,
	},
	["consumable_coffee"] = {
		Label = "Cafea",
        Mode = "DRINK",
        Prop = "p_mugcoffee01x",
        Metabolism = {hunger = false, thirsty = 20, stress = -60, health = false, stamina = false},
		Times = 3,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["chocolatemilk"] = {
		Label = "Ciocolata cu lapte",
        Mode = "DRINK",
        Prop = "p_mugcoffee01x",
        Metabolism = {hunger = false, thirsty = 15, stress = -5, health = false, stamina = false},
		Times = 3,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["milk"] = {
		Label = "Lapte",
        Mode = "DRINK",
        Prop = "p_mugcoffee01x",
        Metabolism = {hunger = false, thirsty = 10, stress = -5, health = false, stamina = false},
		Times = 3,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["tea"] = {
		Label = "Ceai",
        Mode = "DRINK",
        Prop = "p_mugcoffee01x",
        Metabolism = {hunger = false, thirsty = 15, stress = -10, health = false, stamina = false},
		Times = 3,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["ginsengtea"] = {
		Label = "Ceai Ginseng",
        Mode = "DRINK",
        Prop = "p_mugcoffee01x",
        Metabolism = {hunger = false, thirsty = 15, stress = -5, health = false, stamina = false},
		Times = 3,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["vodka"] = {
		Label = "Vodka",
        Mode = "BOTTLE",
        Prop = "p_bottleredmist01x",
        Metabolism = {hunger = false, thirsty = 20, stress = -10, health = false, stamina = false},
		Times = 4,
        Alcohol = 0.3,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["beer"] = {
		Label = "Bere",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer01a",
        Metabolism = {hunger = false, thirsty = 25, stress = -20, health = false, stamina = false},
		Times = 3,
        Alcohol = 0.2,
        Effect = false,
        OverPowerStamina = 5000, 
        OverPowerHealth = false,    
	},
	["wine"] = {
		Label = "Vin",
        Mode = "BOTTLE",
        Prop = "p_bottleconklin01x",
        Metabolism = {hunger = false, thirsty = 25, stress = -20, health = false, stamina = false},
		Times = 3,
        Alcohol = 0.2,
        Effect = false,
        OverPowerStamina = 5000, 
        OverPowerHealth = false,    
	},
	["whisky"] = {
		Label = "Whisky",
        Mode = "BOTTLE",
        Prop = "p_bottleredmist01x",
        Metabolism = {hunger = false, thirsty = 15, stress = -20, health = false, stamina = false},
		Times = 3,
        Alcohol = 0.4,
        Effect = false,
        OverPowerStamina = 5000, 
        OverPowerHealth = false,    
	},
	["tequila"] = {
		Label = "Tequila",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 15, stress = -20, health = false, stamina = false},
		Times = 3,
        Alcohol = 0.4,
        Effect = false,
        OverPowerStamina = 5000, 
        OverPowerHealth = false,    
	},
	["rum"] = {
		Label = "Rom",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer01x",
        Metabolism = {hunger = false, thirsty = 20, stress = -20, health = false, stamina = false},
		Times = 5,
        Alcohol = 0.2,
        Effect = false,
        OverPowerStamina = 5000, 
        OverPowerHealth = false,    
	},
	["tuica"] = {
		Label = "Tuica",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 20, stress = -20, health = false, stamina = false},
		Times = 3,
        Alcohol = 0.35,
        Effect = false,
        OverPowerStamina = 5000, 
        OverPowerHealth = false,    
	},
    ["Consumable_moonshine_apple"] = {
		Label = "Suc de mere",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
    ["consumable_moonshine_plum"] = {
		Label = "Suc de prune",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
    ["consumable_moonshine_blackberry"] = {
		Label = "Suc de mure",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
    ["consumable_moonshine_wild_cider"] = {
		Label = "Suc de menta",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
    ["consumable_moonshine_raspberry"] = {
		Label = "Suc de zmeura",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
    ["consumable_moonshine_peach"] = {
		Label = "Suc de piersici",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
    ["consumable_moonshine"] = {
		Label = "Suc natural",
        Mode = "BOTTLE",
        Prop = "p_bottlebeer02x",
        Metabolism = {hunger = false, thirsty = 100, stress = -10, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 200, 
        OverPowerHealth = 100,    
	},
	-- DRUGS
	["cigarette"] = {
		Label = "Tigara",
        Mode = "SMOKE",
        Prop = "P_CIGARETTE01X",
        Metabolism = {hunger = false, thirsty = false, stress = -10, health = false, stamina = false},
		Times = 10,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 1.0, 
        OverPowerHealth = 1.0,    
	},
	--[[["cigar"] = {
		Label = "Trabuc",
        Mode = "SMOKE",
        Prop = "p_cigar01x",
        Metabolism = {hunger = false, thirsty = false, stress = -10, health = false, stamina = false},
		Times = 10,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = 1.0, 
        OverPowerHealth = 1.0,    
	},]]
	["joint"] = {
		Label = "Joint",
        Mode = "SMOKE",
        Prop = "P_CIGARETTE01X",
        Metabolism = {hunger = false, thirsty = false, stress = -20, health = false, stamina = false},
		Times = 5,
        Alcohol = false,
        Effect = {"PlayerDrugsHalluc01", 30000},
        OverPowerStamina = 1.0, 
        OverPowerHealth = 1.0,    
	},
	["opium"] = {
		Label = "Opiu",
        Mode = "EAT",
        Prop = "p_package09",
        Metabolism = {hunger = false, thirsty = false, stress = -50, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = {"PlayerSickDoctorsOpinionOutBad", 20000},
        OverPowerStamina = 1000.0, 
        OverPowerHealth = false,    
	},
	["hashish"] = {
		Label = "Hasis",
        Mode = "EAT",
        Prop = "p_package09",
        Metabolism = {hunger = false, thirsty = false, stress = -25, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = {"PlayerDrugsPoisonWell", 15000},
        OverPowerStamina = 100.0, 
        OverPowerHealth = 100.0,    
	},
	["morphine"] = {
		Label = "Morfina",
        Mode = "SYRINGE",
        Prop = "mp007_p_mp_syringe01x_1",
        Metabolism = {hunger = false, thirsty = false, stress = 25, health = 25, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = {"PlayerSickDoctorsOpinion", 30000},
        OverPowerStamina = 2000.0, 
        OverPowerHealth = false,    
	},
	["heroin"] = {
		Label = "Heroina",
        Mode = "EAT",
        Prop = "p_package09",
        Metabolism = {hunger = false, thirsty = false, stress = 50, health = false, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = {"PlayerKnockout_WeirdoPat", 40000},
        OverPowerStamina = 5000.0, 
        OverPowerHealth = 100.0,    
	},
	-- MEDICINE
	["bandage"] = {
		Label = "Bandaje",
        Mode = "BANDAGE",
        Prop = "p_cs_bandage01x",
        Metabolism = {hunger = false, thirsty = false, stress = -10, health = 50, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["herbmed"] = {
		Label = "Bautura medicinala",
        Mode = "BOTTLE",
        Prop = "p_bottlemedicine09x",
        Metabolism = {hunger = 15, thirsty = 15, stress = -15, health = 15, stamina = 15},
		Times = 2,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
    ["herbal_tonic"] = {
		Label = "Amestec Plante",
        Mode = "BOTTLE",
        Prop = "p_bottlemedicine09x",
        Metabolism = {hunger = 15, thirsty = 15, stress = -15, health = 15, stamina = 15},
		Times = 2,
        Alcohol = false,
        Effect = false,
        OverPowerStamina = false, 
        OverPowerHealth = false,    
	},
	["blutonic"] = {
		Label = "Blu Tonic",
        Mode = "BOTTLE",
        Prop = "p_bottlemedicine01x",
        Metabolism = {hunger = false, thirsty = 15, stress = -25, health = 25, stamina = 25},
		Times = 2,
        Alcohol = false,
        Effect = {"MP_ArrowDisorient", 15000},
        OverPowerStamina = 5000.0, 
        OverPowerHealth = false,    
	},
	["mircacleelyxir"] = {
		Label = "Elixir Miraculos",
        Mode = "BOTTLE",
        Prop = "p_bottlemedicine25x",
        Metabolism = {hunger = false, thirsty = 15, stress = 1, health = 100, stamina = false},
		Times = 1,
        Alcohol = false,
        Effect = {"PlayerSickDoctorsOpinionOutGood", 20000},
        OverPowerStamina = 5000.0, 
        OverPowerHealth = 100.0,    
	},
}
    

}

--=========================================================================
-- TRANSLATIONS
-- These messages are used when players consume/drop items.
--=========================================================================

TR = {
    ["drop"] = "Arunca",
    ["smoke"] = "Fumeaza",  
    ["youdrink"] = "You threw it almost full the ",
    ["youdrinkfull"] = "You drank the whole bottle of ",
	["youeat"] = "You just eated a ",
	["youbowlfull"] = "You eat the entire bowl of ",
	["youbowl"] = "You get a taset from the bowl, and drop almost full the ",
	["youbandage"] = "You healed a little with ",
	["yousyringe"] = "You injected yourself with ",
    ["you_drunk"] = "You got DRUNK !",
    ["you_not_drunk"] = "You are not anymore DRUNK ! YUHU...",
    ["youdrop"] = "You droped the ",
}

function NOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000)
end

--[[
===========================================================================
EXPORTS / EVENT USAGE
===========================================================================

PLAYER METABOLISM
1) exports["SS-Metabolism"]:GetStress()
   Returns current stress value from 0 to 100.

2) exports["SS-Metabolism"]:AddStress(amount)
   Adds stress. Example: exports["SS-Metabolism"]:AddStress(10)

3) exports["SS-Metabolism"]:RemoveStress(amount)
   Removes stress. Example: exports["SS-Metabolism"]:RemoveStress(10)

4) exports["SS-Metabolism"]:GetThirsty()
   Returns current thirsty value from 0 to 100.

5) exports["SS-Metabolism"]:AddThirsty(amount)
   Adds thirst. Example: exports["SS-Metabolism"]:AddThirsty(20)

6) exports["SS-Metabolism"]:RemoveThirsty(amount)
   Removes thirst. Example: exports["SS-Metabolism"]:RemoveThirsty(20)

7) exports["SS-Metabolism"]:GetHungry()
   Returns current hungry value from 0 to 100.

8) exports["SS-Metabolism"]:AddHungry(amount)
   Adds food. Example: exports["SS-Metabolism"]:AddHungry(20)

9) exports["SS-Metabolism"]:RemoveHungry(amount)
   Removes food. Example: exports["SS-Metabolism"]:RemoveHungry(20)

REPUTATION
10) exports["SS-Metabolism"]:GetRep()
    Returns reputation level from 0 to 10.

11) exports["SS-Metabolism"]:AddRep(amount)
    Adds internal reputation points. Internal max is 1000.

12) exports["SS-Metabolism"]:RemoveRep(amount)
    Removes internal reputation points.

HORSE METABOLISM
13) exports["SS-Metabolism"]:GetHorseHungry()
14) exports["SS-Metabolism"]:AddHorseHungry(amount)
15) exports["SS-Metabolism"]:RemoveHorseHungry(amount)

16) exports["SS-Metabolism"]:GetHorseThirsty()
17) exports["SS-Metabolism"]:AddHorseThirsty(amount)
18) exports["SS-Metabolism"]:RemoveHorseThirsty(amount)

HOUSING HUD
19) exports["SS-Metabolism"]:SetHousing(mode, number)
    mode 0 = white/default, mode 1 = green, mode 2 = red.
    number is shown in the small badge.

20) exports["SS-Metabolism"]:HousingIcon(icon)
    Uses Config.HouseIcons[icon]. Example: "stash", "outfit", "crafting".

NUI FOCUS HELPERS
TriggerEvent("SS-Metabolism:setNuiFocus", true)
TriggerEvent("SS-Metabolism:setNuiFocus", false)

DISEASE / CUSTOM HEALTH ICON
TriggerEvent("SS-METABOLISM:CLIENT:DISEASE", icon)
Example: TriggerEvent("SS-METABOLISM:CLIENT:DISEASE", "snakepoison")
The image must exist in UI/img/health as icon.png, or use "default".
===========================================================================
]]
```
{% endcode %}

