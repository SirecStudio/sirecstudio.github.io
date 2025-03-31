# Configuration File

{% code overflow="wrap" %}
```lua
-- Author 'SIREC#0001'
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd --

Config = {
Dev = true,
Metabolism = false, -- IF USE SS-METABOLISM SET TRUE
WebHook = "",
    
SearchAllow = {"Maresal", "Judecator", "Guvernator", "PolitiaFederala", "Detectiv", "PolitieFrontiera", "OfiterValentine", "SerifValentine", "OfiterAnnesburg", "SerifAnnesburg", "OfiterRhodes", "SerifRhodes", "OfiterBlackWater", "SerifBlackWater"}, -- JOBS THAT CAN SEARCH EVERYWHERE EVERYTIME
GradePolice = 9, -- THIS GRADE OR HIGHER CAN TAKE HORSES FROM MARKET FOR 0€ (THIS HELPS TO GET STOLED HORSES AND GIVE BACK TO OWNER)
----------------------------------------CONTROLS-------------------------------------------------   
StartDrinkButton = 0xC7B5340A,
StartMountButton = 0xC7B5340A,
StopTrainingButton = 0xFF8109D8,
StartBreedingButton = 0xFF8109D8,
HorsePutPelts = 0x06052D11,
HorseGetPelts = 0x760A9C6F,
HorseOpenStash = 0xE30CD707,
WagonSendAway = 0x06052D11,
WagonGetCargo = 0x760A9C6F,
WagonDropCargo = 0x4BC9DABB,
WagonOpenStash = 0xFF8109D8,
WagonOutfits = 0xDB096B85,
TransferHorse = 0x4BC9DABB, --0x06052D11, --0x4BC9DABB,
SellHorse = 0xFF8109D8,
ActiveIt = 0xC7B5340A,
CustomIt = 0x760A9C6F,
CallWagon = 0xF3830D8E,
CallHorse = 0x24978A28,
MarketWithdraw = 0x760A9C6F,
MarketBuy = 0xC7B5340A,
SellMarket = 0x9959A6F0,
SetTarpaulin = false, -- NEW 3.7

--------------------------------------EXTRA EQUIP--------------------------------------------------
ExtraEquip = {
	["extrabag"] = {Hash = 0xEE1C8EF2, Stash = 2}, -- EXTRA BAGS INVENTORY ( * Stash / Double The Actual Invenory) horsebags1 NEW 4.0
	["flameshoes"] = {Hash = "", Flame = true}, -- Flamming Shoes (Change only the item) NEW 4.0
	["horseloadout1"] = {Hash = 0x2459E0BD}, -- HUGE BAGS ON HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horseloadout2"] = {Hash = 0x951FB0EB}, -- HUGE BAGS ON BACK HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horseloasout3"] = {Hash = 0xDCC33A7C}, -- HUGE CHESTS ON HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horseloadout4"] = {Hash = 0x4514190C}, -- HUGE MOONSHINE ON HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horseloadout5"] = {Hash = 0x460A74C6}, -- HUGE HUNTING ON HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horseloadout6"] = {Hash = 0x56F11EF7}, -- HUGE MINING TOOLS ON HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horseloadout7"] = {Hash = 0xDA9244A3}, -- HUGE THINGS ON HORSE (You can add extra stash, but people can ABUSE it) NEW 4.0
	["horsearrow"] = {Hash = 0xABB8A3F1}, -- ARROWS IN HORSE NEW 4.0
	["horseblanket"] = {Hash = 0x9F275113}, -- HORSE SADDLE BLANKET  NEW 4.0
	["horsebag1"] = {Hash = 0x55CEE4B7}, -- SUGAR BAGS NEW 4.0
	["horsemask2"] = {Hash = 0x79DBC798}, -- Blanket Mask NEW 4.0
	["horsemask1"] = {Hash = 	0x5A510883}, -- COBRA MASK NEW 4.0
	["horseflag"] = {Hash = 0x03CE3847}, --FLAG ON HORSE NEW 4.0

	["horselantern"] = {Hash = 0xF08D4D50}, -- HORSE LANTERN NEW 4.0
	["horsetorch"] = {Hash = 0xEA0F04C9}, -- TORCH ON HORSE
	["legendarysaddle"] = {Hash = 0xD3C7AE66},  -- LEGENDARY SADDLE
	["blanketwolf"] = {Hash = 0xD28F9C56}, -- WOLF BLANKET
	["blanketbear"] = { Hash = 0xE0C338BD}, -- Blanket Bear
	["saddlestandard"] = {Hash = 0xC6AE9EAB},  -- Saddle Standard
},
    
------------------------------------- HORSE SETTINGS ---------------------------------------------

-- General Settings
UseDefaultStats = false, -- Use default stats for horses, or what you set in horses.lua ?
HorseEquipmentsWithGold = false, -- (true = Gold, false = Money) Set payment type for horse equipment.
TimeToDrink = 10000, -- Time (ms) it takes for the horse to drink.
DrinkAddHealth = 10, -- Amount of health added when the horse drinks.
DrinkAddStamina = 35, -- Amount of stamina added when the horse drinks.
AttackEnemies = 3500, -- Horse attacks enemies when called, if it has 3500 EXP. Set false to disable.
StandbySit = 60, -- Time (seconds) for the horse to sit down when idle. Set false to disable.

-- Visibility Settings
HideNameHorseToOthers = true, -- Hides the horse's name and shows its ID to other players.
ShowCustomNameToOthers = false, -- Shows custom text instead of the horse's name/ID to others. Set false to disable.

-- Horse Ownership Limits
MaxHorses = 5, -- Maximum horses for normal players.
TrainersMaxHorses = 8, -- Maximum horses for trainers.
ByPassLimit = { -- Groups that bypass horse ownership limits.
    ["vipbronze"] = 8,
    ["vipsilver"] = 10,
    ["vipgold"] = 12,
},

-- Horse Attributes
BuyHorseAge = {10, 25}, -- Random age range for new horses purchased from stables.
CallHorseOnlyInCities = false, -- Call horses only in cities or near stables. (true = cities only)
SendHorseOnlyInCities = false, -- Send horses away only in cities or near stables. (true = cities only)

-- Horse Cooldowns
ReCallCooldown = 1, -- Seconds before you can call the horse again. Set false to disable.
ReSendCooldown = 1, -- Seconds before you can send the horse away again. Set false to disable.

-- Behavior and Interaction
ChanceSendAway = 50, -- Percentage chance to send away unknown or agitated horses.
CallDistanceToRoads = 100.0, -- Maximum distance (in meters) to check for road spawn for wagons.
LassoHorse = true, -- Determines if horses can be lassoed.
ReviveItem = "horserevive", -- Item required to revive horses.
ChangeToSearchBags = 50, -- Chance (%) for the horse to fail searching players' bags (ex: 50% + horse level bonus).

-- Horse Market Settings
HorseSellPrice = 50, -- Percentage of original value when selling a horse.
BlacklistCities = {"Annesburg", "Blackwater", "Rhodes", "Siska", "StDenis", "Strawberry", "Valentine"}, -- Cities where certain actions are restricted.
TransferHorseBlacklist = { -- Horses that cannot be transferred.
    "a_c_horse_arabian_white",
    "a_c_horse_belgian_mealychestnut",
    "a_c_horse_thoroughbred_reversedappleblack",
    "a_c_horse_turkoman_grey",
    "a_c_horse_turkoman_silver",
},
SellHorseBlacklist = {}, -- Horses that cannot be sold.
SellMarketHorseBlacklist = { -- Horses that cannot be sold at the market.
    "a_c_horse_arabian_white",
    "a_c_horse_belgian_mealychestnut",
    "a_c_horse_thoroughbred_reversedappleblack",
    "a_c_horse_turkoman_grey",
    "a_c_horse_turkoman_silver",
},

-- Cities Where Horses Can Be Called/Sent
AllowedToCallCity = {"Annesburg", "Armadillo", "Blackwater", "Rhodes", "StDenis", "Strawberry", "Tumbleweed", "Valentine", "Vanhorn"},
AllowedToSendCity = {"Annesburg", "Armadillo", "Blackwater", "Rhodes", "StDenis", "Strawberry", "Tumbleweed", "Valentine", "Vanhorn"},

-- Horse Tricks
HorseTricksKey = 0x63A38F2C, -- Default is when you pat you horse the menu come's up !
HorseTricksCommand = "tricks", -- Horse tricks command, insert the command to enable or false to disable !
HorseTrickDistance = 15, -- Distance between player and horse to can make the horse do the tricks !
HorseTricks = {
    [1] = {Tittle = "Strange Walk", Anim = "horse_crossing_river_horse", Dict = "amb_creature_mammal@world_horse_crossing_river", Time = 5000, Flag = 0, Exp = 500},
    [2] = {Tittle = "Pasture", Anim = "base", Dict = "amb_creature_mammal@world_horse_grazing@base", Time = 30000, Flag = 0, Exp = 500},
    [3] = {Tittle = "Fake Injured", Anim = "base", Dict = "amb_creature_mammal@world_horse_injured_on_ground@base", Time = -1, Flag = 1, Exp = 3500},
    [4] = {Tittle = "Resting", Anim = "base", Dict = "amb_creature_mammal@world_horse_resting@base", Time = -1, Flag = 0, Exp = 1500},
    [5] = {Tittle = "Sleeping", Anim = "base", Dict = "amb_creature_mammal@world_horse_sleeping@base", Time = -1, Flag = 1, Exp = 2000},
    [6] = {Tittle = "Wallow", Anim = "base", Dict = "amb_creature_mammal@world_horse_wallow_shake@base", Time = 30000, Flag = 0, Exp = 4000},
    [7] = {Tittle = "Hop", Anim = "hop_with_rearing", Dict = "amb_creature_mammal@world_horse_rearing", Time = -1, Flag = 0, Exp = 4000},
},

-- Horse Thief
HidenStoledHorsesBlip = -1456209806, -- Blip of Abandoned Stable to bring stoled horses ( ONLY HORSETRAINERS JOBS CAN SEE IT )
HidenStoledHorses = {-5520.1357421875, -3044.590087890625, -3.38769245147705}, -- FALSE TO DISABLE / OR COORDS FOR ENABLE {x, y, z} !
HidenStoledHorsesName = "Grajd Abandonat", -- Blip name of abandoned stable
HorsesBlacklist = {"a_c_horse_arabian_white", "a_c_horse_belgian_mealychestnut", "a_c_horse_thoroughbred_reversedappleblack", "a_c_horse_turkoman_grey", "a_c_horse_turkoman_silver"},

-- Horse Food
Feed = { -- ITEMNAME / LABEL ITEM / BOOST / HEALTH AMOUNT / STAMINA AMOUNT
["corn"] = {label = "Porumb", boost = false, health = 30, stamina = 10, thirsty = 10, hungry = 45}, -- To disable stamina or health use false , Or set the amount ! 
["Wild_Carrot"] = {label = "Morcov",  boost = false, health = 10, stamina = 30, thirsty = 10, hungry = 45}, -- To disable stamina or health use false , Or set the amount ! 
["consumable_haycube"] =  {label = "HayCube",  boost = false, health = 20, stamina = 20, thirsty = 10, hungry = 45}, -- To disable stamina or health use false , Or set the amount ! 
["stim"] =  {label = "Stimulent Cal",  boost = true, health = 100, stamina = 100, thirsty = 10, hungry = 45}, --To disable stamina or health use false , Or set the amount ! 
},
    
------------------------------------- WAGON SETTINGS ---------------------------------------------

-- General Settings
WagonEquipmentsWithGold = false, -- (true = Gold, false = Money) Set payment type for wagon equipment.
WagonLowHealth = 100, -- Health threshold below which wagons become undrivable.
ActiveLastPosition = true, -- Save the last position (city, stable, house, or clan) and only allow calling wagons from there.

-- Outfit Settings
EnableOutfits = "xakra_clothingstores:OutfitsClothingStoreMenu", -- Trigger to open outfits menu. Set false to disable.

-- Housing and Clan Integration
SSHousing = false, -- If using SS-Housing, allow calling/sending wagons from the house.
SSClan = false, -- If using SS-Clan, allow calling/sending wagons from the clan.

-- Wagon Repair Settings
HammerRepair = "ironhammer", -- Item used to repair the wagon.
HammerRepairAnimation = {dict = "", anim = ""}, -- Animation dict and anim, only if scenario is false !
HammerRepairScenario = "PROP_HUMAN_REPAIR_WAGON_WHEEL_ON_LARGE", -- Scenario to use, put false to use animation instead !
HammerRepairTime = 5000, -- Time (ms) required to repair the wagon.
HammerAddWagonHealth = 250, -- Add 250 on every repair, max is 1000 ! Adjust how you like
HammerRepairNeeds = {"nails", 4, "Cuie"}, -- Required items to repair (e.g., {"ITEM", AMOUNT, "LABEL"}).

-- Location Restrictions
CallWagonOnlyInCities = true, -- Allow calling wagons only in cities or near stables.
SendWagonOnlyInCities = true, -- Allow sending wagons away only in cities or near stables.
WagonDistanceToRoads = 100.0, -- Maximum distance to check for roads when spawning a wagon. Set false to disable road checks.

-- Distance and Cooldowns
MaxDistanceToCall = 100.0, -- Maximum distance to call the wagon if it's already spawned. Otherwise, respawn it.

-- Market Settings
MaxMarketPrice = 2, -- Max price for horses when you sell in Market, horse price x 2, wich is double set as you like !
WagonSellPrice = 25, -- Percentage of the original price when selling a wagon. (NEW)
BlackListCityLockpick = {'Annesburg', 'Blackwater', 'Rhodes', 'Siska', 'StDenis', 'Strawberry', 'Valentine'}, -- Cities where lockpicking wagons is restricted.

-- Blacklists
TransferWagonBlacklist = { -- Wagons that cannot be transferred.
    "chuckwagon000X",
    "buggy01",
},
SellWagonBlacklist = { -- Wagons that cannot be sold.
    "chuckwagon000X",
    "buggy01",
},

---------------------------------------- TRAINING SETTINGS ----------------------------------------------
Experience = { -- Experience affects stamina generation and depletion ! 
	[5] = { -- Full Training 4000 EXP
		RegenStamina = 3.0, -- Regeneration x3.0
		DecreaseStamina = 1.0, -- Decrease stamina x1.0
                
	},
	[4] = { -- Effects over 3000 EXP
		RegenStamina = 2.5, -- Regeneration x2.5
		DecreaseStamina = 1.5, -- Decrease stamina x1.5
                
	},
	[3] = { -- Effects over 2000 EXP
		RegenStamina = 2.0, -- Regeneration x2.0
		DecreaseStamina = 2.0, -- Decrease stamina x2.0
                
	},
	[2] = { -- Effects over 1000 EXP
		RegenStamina = 1.5, -- Regeneration x1.5
		DecreaseStamina = 2.5, -- Decrease stamina x2.5
                
	},
	[1] = { -- Effects under 1000 EXP
		RegenStamina = 1.0, -- Regeneration x1.0
		DecreaseStamina = 3.0, -- Decrease stamina x3.0
                
	},
},

Training = {
    -- General Settings
    TrainerBookItem = "horselist", -- Item used by trainers to open a list with all horses and see if they are stolen (* near the serial means stolen).
    Jobs = {"HorseTrainerBW", "HorseTrainerRH", "HorseTrainerSD", "HorseTrainerVAL"}, -- Jobs for horse trainers.
    ShoesTime = 5000, -- Time (ms) for the horseshoe placement animation duration.
    Whip = "horsetrain", -- Whip item used to start training the horses.
    MinStamina = 20, -- If the horse's stamina drops below this value, the training will stop, and the trainer will fall off the horse!
    -- Training Notes:
    -- Training does not add stamina directly but will decrease stamina consumption and speed up its recovery.
    -- To add more stamina points, horseshoes must be equipped.
},

-- Training Type Selection
ChoiceTraining = false, -- (true = Allows choosing the training type when using the whip, false = Uses the training type set in each stable).

HorseTraining = {
    -- Type 1: Step Training (Walk/Run/Jump through markers)
    [1] = {
        ["Valentine"] = { -- Stable Name
            Enable = true, -- Enable/Disable this route.
            CurrentStepColor = {255, 0, 0}, -- Current step color (RGB).
            NextStepColor = {0, 0, 0}, -- Next step color (RGB).
            Exp = 150, -- EXP gained after completing the route.
            Steps = { -- Marker coordinates (Marker: 0x6903B113 for ground, 0xEC032ADD for circles).
                [1] = {-386.017578, 786.026368, 114.921630, 0.0, 0.0, 90.0, 0x6903B113},
                [2] = {-395.182404, 787.595582, 115.005860, 0.0, 0.0, 90.0, 0x6903B113},
                [3] = {-398.927460, 780.250550, 114.904786, 0.0, 0.0, 90.0, 0x6903B113},
                [4] = {-386.887908, 774.092286, 114.921630, 0.0, 0.0, 90.0, 0x6903B113},
                [5] = {-396.909882, 769.041748, 114.972168, 0.0, 0.0, 90.0, 0x6903B113},
                [6] = {-398.136260, 777.863708, 114.871094, 0.0, 0.0, 90.0, 0x6903B113},
                [7] = {-394.496704, 788.400024, 115.022706, 0.0, 0.0, 90.0, 0x6903B113},
                [8] = {-386.030762, 779.406616, 116.101074, 0.0, 0.0, 180.0, 0xEC032ADD},
                [9] = {-392.769226, 768.870300, 114.904786, 0.0, 0.0, 90.0, 0x6903B113},
                [10] = {-390.883514, 778.232972, 114.786866, 0.0, 0.0, 90.0, 0x6903B113},
            }
        },
        ["BlackWater"] = { -- Stable Name
            Enable = true, -- Enable/Disable this route.
            CurrentStepColor = {255, 0, 0}, -- Current step color (RGB).
            NextStepColor = {0, 0, 0}, -- Next step color (RGB).
            Exp = 150, -- EXP gained after completing the route.
            Steps = { -- Marker coordinates (Marker: 0x6903B113 for ground, 0xEC032ADD for circles).
                [1] = {-887.3292236328125, -1378.822509765625, 42.88726196289062, 0.0, 0.0, 90.0, 0x6903B113},
                [2] = {-889.078125, -1365.821044921875, 42.64348373413086, 0.0, 0.0, 90.0, 0x6903B113},
                [3] = {-889.0767211914062, -1351.7811279296875, 42.41520843505859, 0.0, 0.0, 90.0, 0x6903B113},
                [4] = {-872.6477661132812, -1351.5440673828125, 42.42537460327148, 0.0, 0.0, 90.0, 0x6903B113},
                [5] = {-863.9517211914062, -1343.7161865234375, 42.51334533691406, 0.0, 0.0, 90.0, 0x6903B113},
                [6] = {-859.0445556640625, -1321.2781982421875, 42.28737411499023, 0.0, 0.0, 90.0, 0x6903B113},
                [7] = {-847.3763427734375, -1334.6639404296875, 42.47765884399414, 0.0, 0.0, 90.0, 0x6903B113},
                [8] = {-848.0678100585938, -1359.25, 42.52935943603515, 0.0, 0.0, 90.0, 0x6903B113},
                [9] = {-855.635986328125, -1383.1864013671875, 42.64427337646484, 0.0, 0.0, 90.0, 0x6903B113},
                [10] = {-875.3466186523438, -1384.2388916015625, 42.6351676940918, 0.0, 0.0, 90.0, 0x6903B113},
            }
        },
    },

    -- Type 2: Random Action Training
    [2] = {
        Enable = true, -- Enable/Disable this type of training.
        StepsTime = {6, 9}, -- Time (seconds) between steps.
        StepsNeed = {5, 10}, -- Random number of steps required to complete the training.
        ExpWhenWalking = 10, -- EXP gained when walking with the horse.
        ExpWhenRunning = 15, -- EXP gained when running with the horse.
        ExpWhenRearUp = 15, -- EXP gained when rearing up.
        ExpWhenTurnRight = 30, -- EXP gained when turning right.
        ExpWhenTurnLeft = 30, -- EXP gained when turning left.
        ExpWhenDance = 20, -- EXP gained when making the horse dance.
        ExpWhenJumping = 15, -- EXP gained when jumping.
        Steps = {
            [1] = {action = "JUMP", waittime = 3, info = "You need to JUMP with your horse."},
            [2] = {action = "WALK", waittime = 4, info = "You need to WALK with your horse."},
            [3] = {action = "RUN", waittime = 5, info = "You need to RUN with your horse."},
            [4] = {action = "DANCE", waittime = 4, info = "You need to DANCE with your horse."},
            [5] = {action = "TURN LEFT", waittime = 2, info = "You need to TURN LEFT with your horse."},
            [6] = {action = "TURN RIGHT", waittime = 2, info = "You need to TURN RIGHT with your horse."},
            [7] = {action = "REAR UP", waittime = 5, info = "You need to REAR UP with your horse."},
        }
    },

    -- Type 3: Free Training
    [3] = {
        Enable = true, -- Enable/Disable this type of training.
        ExpWhenWalking = 0.01, -- EXP per step while walking.
        ExpWhenRunning = 0.03, -- EXP per step while running.
        ExpWhenSkid = 30, -- EXP for skidding.
        ExpWhenRearUp = 5, -- EXP for rearing up.
    },
},

-- Horseshoe Settings
Shoes = { -- Horseshoes increase stamina. Losing a horseshoe reduces stamina points.
    ["0"] = {label = "No Horseshoes", km = 0},
    ["ironhorseshoe"] = {label = "Iron Horseshoe", km = 20000},
    ["silverhorseshoe"] = {label = "Silver Horseshoe", km = 40000},
    ["goldhorseshoe"] = {label = "Gold Horseshoe", km = 80000},
},

---------------------------------------- BREEDING SETTINGS -------------------------------------------      

Breeding = {
    -- General Settings
    Jobs = {"HorseTrainerBW", "HorseTrainerRH", "HorseTrainerSD", "HorseTrainerVAL"}, -- Jobs allowed for breeding.
    AllowCross = true, -- If true, the foal will have a custom appearance (24 custom appearances available).
    Pill = "breedpills", -- The item (pill) required to start the breeding process (used for male horses in training zones).
    Brush = "horsebrush", -- The item (brush) used to clean horses.
    Chance = 50, -- Percentage chance to successfully start breeding (otherwise the horse will run away, and you must try again).
    BreedTime = 30000, -- Time (ms) the horse remains in the breeding animation if successful.
    ChanceFoal = 50, -- Percentage chance for the foal to inherit the father's race.
    ChanceSex = 50, -- Percentage chance for the foal to be male or female.
    BreedWaitTime = 10, -- Days to wait before the foal is born.
    Handicap = 2, -- Reduction factor for stamina, speed, and acceleration for pregnant female horses.
    CheckBreed = 1, -- Frequency (in hours) to check if breeding is complete.
    StartRiding = 4, -- Number of days before the foal can be ridden.
    StartBreeding = 6, -- Number of days before the foal can begin breeding.
    StartTraining = 8, -- Number of days before the foal can begin training.
    StartAdult = 10, -- Number of days before the foal becomes an adult and can equip items.
    StartOld = 75, -- Number of days before the horse becomes old (status changes to "Old" with a scale of 1.1).
    StartDead = 95, -- Number of days before the horse dies.
    StartDeleteIt = 100, -- Number of days before the horse is deleted from the server.
    StopBreeding = 60, -- Number of days after which the horse can no longer breed.
    EnableBlackLists = true, -- Enable breeding blacklists (false to allow all horses to breed freely).

    -- Breeding Blacklists
    -- Only horses within the same category can breed. If a horse is not listed in any category, it cannot breed.
    BlackLists = {
        -- Category 1: American Paint, Appaloosa, and other breeds
        [1] = {
            "a_c_horse_americanpaint_greyovero", "a_c_horse_americanpaint_overo", "a_c_horse_americanpaint_splashedwhite", 
            "a_c_horse_americanpaint_tobiano", "a_c_horse_americanstandardbred_silvertailbuckskin", 
            "a_c_horse_americanstandardbred_palominodapple", "a_c_horse_americanstandardbred_buckskin", 
            "a_c_horse_americanstandardbred_black", "a_c_horse_andalusian_darkbay", "a_c_horse_andalusian_perlino", 
            "a_c_horse_andalusian_rosegray", "a_c_horse_appaloosa_brownleopard", "a_c_horse_appaloosa_leopard", 
            "a_c_horse_appaloosa_fewspotted_pc", "a_c_horse_appaloosa_leopardblanket", "a_c_horse_appaloosa_blanket", 
            "a_c_horse_ardennes_strawberryroan", "a_c_horse_ardennes_irongreyroan", "a_c_horse_ardennes_bayroan", 
            "a_c_horse_belgian_blondchestnut", "a_c_horse_belgian_mealychestnut", "a_c_horse_dutchwarmblood_chocolateroan", 
            "a_c_horse_dutchwarmblood_sealbrown", "a_c_horse_dutchwarmblood_sootybuckskin", 
            "a_c_horse_hungarianhalfbred_darkdapplegrey", "a_c_horse_hungarianhalfbred_flaxenchestnut", 
            "a_c_horse_hungarianhalfbred_liverchestnut", "a_c_horse_hungarianhalfbred_piebaldtobiano", 
            "a_c_horse_kentuckysaddle_black", "a_c_horse_kentuckysaddle_buttermilkbuckskin_pc", 
            "a_c_horse_kentuckysaddle_chestnutpinto", "a_c_horse_kentuckysaddle_grey", "a_c_horse_kentuckysaddle_silverbay", 
            "a_c_horse_morgan_bay", "a_c_horse_morgan_bayroan", "a_c_horse_morgan_flaxenchestnut", 
            "a_c_horse_morgan_palomino", "a_c_horse_morgan_liverchestnut_pc", "A_C_Horse_MP_Mangy_Backup", 
            "a_c_horse_nokota_blueroan", "a_c_horse_nokota_reversedappleroan", "a_c_horse_nokota_whiteroan", 
            "a_c_horse_shire_darkbay", "a_c_horse_shire_lightgrey", "a_c_horse_shire_ravenblack", 
            "a_c_horse_suffolkpunch_redchestnut", "a_c_horse_suffolkpunch_sorrel", "a_c_horse_tennesseewalker_blackrabicano", 
            "a_c_horse_tennesseewalker_chestnut", "a_c_horse_tennesseewalker_dapplebay", "a_c_horse_tennesseewalker_flaxenroan", 
            "a_c_horse_tennesseewalker_goldpalomino_pc", "a_c_horse_tennesseewalker_mahoganybay", 
            "a_c_horse_tennesseewalker_redroan"
        },

        -- Category 2: Gypsy Cob, Kladruber, Thoroughbred, and similar breeds
        [2] = {
            "a_c_horse_gypsycob_splashedpiebald", "a_c_horse_gypsycob_splashedbay", "a_c_horse_gypsycob_palominoblagdon", 
            "a_c_horse_gypsycob_skewbald", "a_c_horse_gypsycob_piebald", "a_c_horse_gypsycob_whiteblagdon", 
            "a_c_horse_kladruber_black", "a_c_horse_kladruber_cremello", "a_c_horse_kladruber_dapplerosegrey", 
            "a_c_horse_kladruber_grey", "a_c_horse_kladruber_silver", "a_c_horse_kladruber_white", 
            "a_c_horse_thoroughbred_blackchestnut", "a_c_horse_thoroughbred_bloodbay", "a_c_horse_thoroughbred_brindle", 
            "a_c_horse_thoroughbred_dapplegrey", "a_c_horse_breton_sealbrown", "a_c_horse_breton_redroan", 
            "a_c_horse_breton_steelgrey", "a_c_horse_breton_grullodun", "a_c_horse_breton_mealydapplebay", 
            "a_c_horse_breton_sorrel", "a_c_horse_norfolkroadster_spottedtricolor", 
            "a_c_horse_norfolkroadster_speckledgrey", "a_c_horse_norfolkroadster_rosegrey", 
            "a_c_horse_norfolkroadster_piebaldroan", "a_c_horse_norfolkroadster_dappledbuckskin", 
            "a_c_horse_norfolkroadster_black"
        },

        -- Category 3: Arabian, Missouri Fox Trotter, Mustang, Turkoman, and similar breeds
        [3] = {
            "a_c_horse_arabian_rosegreybay", "a_c_horse_arabian_black", "a_c_horse_arabian_warpedbrindle_pc", 
            "a_c_horse_arabian_redchestnut", "a_c_horse_arabian_redchestnut_pc", "a_c_horse_arabian_grey", 
            "a_c_horse_gang_dutch", "a_c_horse_missourifoxtrotter_amberchampagne", 
            "a_c_horse_missourifoxtrotter_blacktovero", "a_c_horse_missourifoxtrotter_blueroan", 
            "a_c_horse_missourifoxtrotter_buckskinbrindle", "a_c_horse_missourifoxtrotter_dapplegrey", 
            "a_c_horse_missourifoxtrotter_sablechampagne", "a_c_horse_missourifoxtrotter_silverdapplepinto", 
            "a_c_horse_mustang_blackovero", "a_c_horse_mustang_buckskin", "a_c_horse_mustang_chestnuttovero", 
            "a_c_horse_mustang_goldendun", "a_c_horse_mustang_grullodun", "a_c_horse_mustang_reddunovero", 
            "a_c_horse_mustang_tigerstripedbay", "a_c_horse_mustang_wildbay", "a_c_horse_turkoman_black", 
            "a_c_horse_turkoman_chestnut", "a_c_horse_turkoman_darkbay", "a_c_horse_turkoman_gold", 
            "a_c_horse_turkoman_perlino", "a_c_horse_criollo_baybrindle", "a_c_horse_criollo_bayframeovero", 
            "a_c_horse_criollo_blueroanovero", "a_c_horse_criollo_dun", "a_c_horse_criollo_marblesabino", 
            "a_c_horse_criollo_sorrelovero"
        }
    }
},

------------------------------------ TAMING SETTINGS ------------------------------------------

Taming = {
    -- Allowed Jobs for Taming Horses
    Jobs = {
        "HorseTrainerBW", "HorseTrainerRH", "HorseTrainerSD", "HorseTrainerVAL", "Marshal", 
        "Judge", "Governor", "FederalPolice", "Detective", "BorderPolice", "Unemployed", 
        "Gunsmith", "Shaman", "Blacksmith", "BountyHunter", "Doctor", "MayorBlackWater", 
        "MayorRhodes", "MayorSaintDenis", "MayorValentine", "Jeweler", "Forester", 
        "Miner", "ValentineOfficer", "ValentineSheriff", "AnnesburgOfficer", 
        "AnnesburgSheriff", "RhodesOfficer", "RhodesSheriff", "BlackWaterOfficer", 
        "BlackWaterSheriff", "GunsmithBW", "GunsmithVAL", "GunsmithRH", "ResidentDoctorVAL", 
        "ResidentDoctorRH", "ResidentDoctorBW", "PrimaryDoctor", "SpecialistDoctorVAL", 
        "SpecialistDoctorRH", "SpecialistDoctorBW"
    },

    -- Taming Settings
    MaxFails = 2, -- Maximum number of failed attempts before the player is thrown off.
    MaxSucces = 6, -- Number of successful hits required to tame the horse.
    RandomTime = {500, 2500}, -- Random interval (in ms) to display the button prompt.
    ReactionTime = 800, -- Time (in ms) the player has to react to the prompt.
    TamingPrice = 70, -- Percentage of the horse's price required to tame it.
    SellPrice = 3, -- Percentage of the horse's price when selling it.
    TamingAge = {20, 30}, -- The age range (in days) of tamable horses.
},
    
------------------------------------- STABLES SETTINGS --------------------------------------------

    -- General Settings for Training and Breeding Zones
    TrainBreedZoneBlip = -271586249, -- Blip ID for the training and breeding zone
    TrainBreedZoneName = "Training Zone", -- Name of the training and breeding zone

    -- Stable Locations
    Stables = {
        ["1"] = { -- Valentine Stable
            Name = "Valentine",
            CamPos = {-382.25, 769.90, 118.45}, -- Camera Position for stable menu
            Blip = -1456209806, -- Blip ID for the stable location
            MySpot = {-369.6344, 791.5049, 115.0802, -175.34}, -- Location to spawn your horse
            ActiveMyWagon = true, -- Allow wagon usage at this stable
            MyWagonSpot = {-363.7694, 775.3442, 115.2707, -85.71}, -- Location to spawn wagons
            CustomPos = {-377.7004, 770.0306, 115.1071, 5.11}, -- Custom position for specific interactions
            TrainingType = 1, -- 1 = Step Circle, 2 = Follow Steps, 3 = Manual Training
            TrainingPos = {-393.4384, 777.8362, 115.6014}, -- Zone for training and breeding
            Distance = 15, -- Distance for interaction zones
            SellHorses = true, -- Allow horse selling
            SellSpots = {
                [1] = {Pos = {-366.3351, 782.8293, 115.0967, 1.53}}, -- Horse selling position
            },
            SellWagons = true, -- Allow wagon selling
            SellWagonsSpot = {-377.5419, 774.3201, 116.0970, -86.04}, -- Wagon selling position
            SellPlayersHorse = true, -- Enable horse market
            SellPlayersHorseSpot = {-372.0207, 782.5172, 115.0967, 1.53}, -- Horse market position
        },

        ["2"] = { -- BlackWater Stable
            Name = "BlackWater Stable",
            CamPos = {-875.02, -1382.39, 46.45},
            Blip = -1456209806,
            MySpot = {-867.5707, -1370.5565, 42.8182, 0.09},
            ActiveMyWagon = true,
            MyWagonSpot = {-892.8503, -1370.4193, 42.2997, 2.66},
            CustomPos = {-875.1373, -1376.1781, 42.7707, 88.55},
            TrainingType = 3,
            TrainingPos = {-874.5535, -1390.7340, 43.5835},
            Distance = 15,
            SellHorses = true,
            SellSpots = {
                [1] = {Pos = {-867.6696, -1361.9070, 42.7992, -177.77}},
            },
            SellWagons = true,
            SellWagonsSpot = {-883.2468, -1370.1073, 42.2370, -0.70},
            SellPlayersHorse = true,
            SellPlayersHorseSpot = {-861.0592, -1361.6440, 42.7821, -178.53},
        },

        ["3"] = { -- Rhodes Stable
            Name = "Rhodes Stable",
            CamPos = {1430.44, -1311.03, 80.42},
            Blip = -1456209806,
            MySpot = {1440.13, -1299.83, 76.96, 99.97},
            ActiveMyWagon = true,
            MyWagonSpot = {1448.53, -1280.57, 77.72, -162.73},
            CustomPos = {1429.28, -1305.60, 76.90, 102.55},
            TrainingType = 3,
            TrainingPos = {1428.16, -1267.97, 78.81},
            Distance = 15,
            SellHorses = true,
            SellSpots = {
                [1] = {Pos = {1435.69, -1286.11, 76.96, -110.77}},
            },
            SellWagons = true,
            SellWagonsSpot = {1441.68, -1282.59, 77.74, -159.39},
            SellPlayersHorse = true,
            SellPlayersHorseSpot = {1439.21, -1295.22, 76.97, -110.53},
        },

        ["4"] = { -- Van Horn Stable
            Name = "Van Horn Stable",
            CamPos = {2956.79, 763.07, 56.42},
            Blip = -1456209806,
            MySpot = {2961.48, 801.26, 50.61, 178.45},
            ActiveMyWagon = true,
            MyWagonSpot = {2957.07, 808.77, 50.39, 178.81},
            CustomPos = {2966.05, 764.14, 50.53, -2.92},
            TrainingType = 3,
            TrainingPos = {2976.17, 785.56, 51.25},
            Distance = 15,
            SellHorses = true,
            SellSpots = {
                [1] = {Pos = {2967.26, 801.24, 50.63, 165.42}},
            },
            SellWagons = true,
            SellWagonsSpot = {2950.71, 808.99, 51.34, -178.43},
            SellPlayersHorse = false,
            SellPlayersHorseSpot = {2973.10, 801.16, 50.59, -174.61},
        },

        ["5"] = { -- Saint Denis Stable
            Name = "Saint Denis Stable",
            CamPos = {2514.33, -1458.99, 48.39},
            Blip = -1456209806,
            MySpot = {2508.58, -1450.61, 45.58, 103.28},
            ActiveMyWagon = true,
            MyWagonSpot = {2496.29, -1437.53, 46.25, -179.84},
            CustomPos = {2509.19, -1459.23, 45.46, -178.20},
            TrainingType = 3,
            TrainingPos = {2502.48, -1450.64, 46.44},
            Distance = 15,
            SellHorses = true,
            SellSpots = {
                [1] = {Pos = {2508.46, -1444.40, 45.54, 89.69}},
            },
            SellWagons = true,
            SellWagonsSpot = {2487.55, -1446.53, 45.08, 179.40},
            SellPlayersHorse = true,
            SellPlayersHorseSpot = {2508.37, -1438.23, 45.49, 90.00},
        },
    },
}
function NOTIFY(text) --SET YOUR NOTIFYCATIONS
	local VORPCore = exports.vorp_core:GetCore()
	VORPCore.NotifyLeft(Config.Texts["tittle_notification"], text, "generic_textures", "tick", 5000, "COLOR_WHITE")
end 
```
{% endcode %}

