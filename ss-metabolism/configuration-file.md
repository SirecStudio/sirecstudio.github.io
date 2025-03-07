# Configuration File

```lua
Config = {

Dev = true,
CommandSetHud = "sethud", -- MOVE ICONS AND SAVE WITH ESC !
ToggleHud = "shud", -- SHOW/HIDE 
    
Refresh = 20, --REFRESH RATE OF CHECKING METABOLISM AND DO THE ACTIONS (SUGGEST MIN 10-20 ! THIS UPDATE ONLY HUNGRY THIRSTY STRESS DIRTINESS REP!) Health & Stamina are updated instantly !
    
Initial = {-- INITIAL METABOLISM WHEN JOIN THE SERVER
	Thirsty = 90,
	Hungry = 75,
	Stress = 10,
	Reputation = 100,
},
    
UseHealthStamina = true,
UseHorseHealthStamina = true,
RepStats = true,
ActiveNpcHate = true,
RadiusNpc = 20.0,
PeopleStartWalkingAway = 3, -- PEOPLE START WALKING AWAY FROM YOU AT WICH NEGATIVE REPUTATION ?
PeopleStartRunningAway = 2, -- PEOPLE START RUNNING AWAY FROM YOU AT WICH NEGATIVE REPUTATION ?
PeopleStartHateYou = 1, -- PEOPLE START FIGHT/SHOOT YOU AT WICH NEGATIVE REPUTATION ?
BlackListModels = { -- BLACKLIST NPC'S MODEL THAT DON'T INTERACT WITH REPUTATION ACTIONS
    "a_m_m_valtownfolk_01",
    "mp_u_m_m_lom_train_prisoners_01",
    "g_m_m_bountyhunters_01",
    "g_m_m_unibanditos_01",
    "re_street_fight_males_01",
    "U_M_M_BHT_ODRISCOLLSLEEPING",
    "re_street_fight_males_01",
    "mp_g_m_m_bountyhunters_01",
    "U_M_M_BHT_ODRISCOLLMAULED",
    "U_M_M_BHT_ODRISCOLLDRUNK"        
}, 
    
HorseStats = true,
HorseMetabolism = {Thirsty = 1, Hungry = 1}, -- DECREASE EVERY REFRESH TICK !

Temperature = {3, 35}, -- MIN & MAX TEMPERATURE
TemperatureSettings = {
	["HAT"] = 1,
	["SHIRT"] = 2,
	["PANTS"] = 3,
	["BOOTS"] = 2,
	["COAT"] = 5,
	["GLOVES"] = 2,
	["VEST"] = 2,
	["PONCHO"] = 5,
	["MIN"] = {Thirsty = 0, Hungry = 0.5, Stress = 0.2}, --WHAT SHOULD HAPPEN UNDER THIS TEMPERATURE ? REMOVE SETTINGS
	["MAX"] = {Thirsty = 0.5, Hungry = 0, Stress = 0.2},--WHAT SHOULD HAPPEN OVER THIS TEMPERATURE ? REMOVE SETTINGS
},
    
Metabolism = {
	["Idle"] = {Thirsty = 0.4, Hungry = 0.3, Stress = 0}, -- WHAT SHOULD HAPPEN IF IDLE ? HERE ARE ALL FOR - MINUS !
	["Walking"] = {Thirsty = 0.7, Hungry = 0.6, Stress = 0}, --WHAT SHOULD HAPPEN IF WALKINK ? HERE ARE ALL FOR - MINUS !
	["Running"] = {Thirsty = 1.0, Hungry = 0.8, Stress = 0}, --WHAT SHOULD HAPPEN IF RUNNING ? HERE ARE ALL FOR - MINUS !
	["Combat"] = {Thirsty = 1.2, Hungry = 1.2, Stress = 5}, --WHAT SHOULD HAPPEN IF COMBAT ? HERE ARE ALL FOR - MINUS !
	["InBoat"] = {Thirsty = 0.5, Hungry = 0.4, Stress = -5}, --WHAT SHOULD HAPPEN IF INBOAT ? HERE IS  + ONLY STRESS DECREASE RELAX TRIP 
	["InWagon"] = {Thirsty = 0.5, Hungry = 0.4, Stress = -3}, --WHAT SHOULD HAPPEN IF INWAGON ? HERE IS  + ONLY STRESS DECREASE RELAX TRIP 
	["OnMount"] = {Thirsty = 0.4, Hungry = 0.4, Stress = -1}, --WHAT SHOULD HAPPEN IF ONMOUNT ? HERE IS  + ONLY STRESS DECREASE RELAX TRIP 
},
    
KillWhenZero = false, -- KILL THE PLAYER IF HUNGRY OR THIRSTY IS ON 0 ?
DecreaseByStress = 0.2, -- EFFECTS HUNGRY & THIRSTY BY STRESS % OF THE STRESS
    
MetabolismMin = 20,
MetabolismStats = {
	["THIRSTY"] = {Health = 30, Stamina = 10, Stress = 5}, --WHAT SHOULD HAPPEN WHEN THIRSTY UNDER MIN ?
	["HUNGRY"] = {Health = 25, Stamina = 5, Stress = 5}, --WHAT SHOULD HAPPEN WHEN HUNGRY UNDER MIN ?
},

--STRESS
StressRagdoll = true,
RagDollObjects = true, --RAGDOLL IF PLAYER RUN INTO ANY OBJECT ?
RagDollObjectsChance = 85, 
RagDollFalling = false, --RAGDOLL IF PLAYER FALL ?
    
DecreaseFasterStamina1 = 1.5, --DECREASE FASTER STAMINA WHEN STRESS 50% ?
DecreaseFasterStamina2 = 2.0, --DECREASE FASTER STAMINA WHEN STRESS 80% ?
StressChance1 = 50, -- CHANCE TO AFFECT STAMINA DECREASER WHEN STRESS 50%
StressChance2 = 50, -- CHANCE TO AFFECT STAMINA DECREASER WHEN STRESS 80%
    
--[[ EXPORTS
    
exports["SS-Metabolism"]:GetStress()
exports["SS-Metabolism"]:AddStress(AMOUNT)
exports["SS-Metabolism"]:RemoveStress(AMOUNT)
    
exports["SS-Metabolism"]:GetThirsty()
exports["SS-Metabolism"]:AddThirsty(AMOUNT)
exports["SS-Metabolism"]:RemoveThirsty(AMOUNT)
    
exports["SS-Metabolism"]:GetHungry()
exports["SS-Metabolism"]:AddHungry(AMOUNT)
exports["SS-Metabolism"]:RemoveHungry(AMOUNT)
    
exports["SS-Metabolism"]:GetRep()
exports["SS-Metabolism"]:AddRep(AMOUNT)
exports["SS-Metabolism"]:RemoveRep(AMOUNT)
    
exports["SS-Metabolism"]:GetHorseHungry()
exports["SS-Metabolism"]:AddHorseHungry(AMOUNT)
exports["SS-Metabolism"]:RemoveHorseHungry(AMOUNT)
    
exports["SS-Metabolism"]:GetHorseThirsty()
exports["SS-Metabolism"]:AddHorseThirsty(AMOUNT)
exports["SS-Metabolism"]:RemoveHorseThirsty(AMOUNT)
    
EXPORTS ]]
    
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
	}
}
```

