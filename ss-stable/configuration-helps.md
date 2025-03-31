# Configuration Helps

## SS-Stable Configuration Guide

This page documents the full configuration of the **SS-Stable** script for RedM. Every setting has been carefully explained to help server owners and developers fully understand and customize the system to their needs.

***

### General Settings

* `Dev`: Enables developer mode. Useful for debugging.
* `Metabolism`: Set to `true` if you use **SS-Metabolism**; this enables integration.
* `WebHook`: Set a webhook URL if you want to receive logs (e.g., training, breeding) on Discord.

### Permissions and Access

* `SearchAllow`: List of job names that are allowed to search everywhere and anytime.
* `GradePolice`: Officers with this grade or higher can withdraw stolen horses for free from the market.

### Control Bindings

Each key is mapped to a specific in-game action. These values use hexadecimal key hashes from RedM.

| Action              | Default Key Hash |
| ------------------- | ---------------- |
| StartDrinkButton    | 0xC7B5340A       |
| StartMountButton    | 0xC7B5340A       |
| StopTrainingButton  | 0xFF8109D8       |
| StartBreedingButton | 0xFF8109D8       |
| HorsePutPelts       | 0x06052D11       |
| HorseGetPelts       | 0x760A9C6F       |
| HorseOpenStash      | 0xE30CD707       |
| WagonSendAway       | 0x06052D11       |
| WagonGetCargo       | 0x760A9C6F       |
| WagonDropCargo      | 0x4BC9DABB       |
| WagonOpenStash      | 0xFF8109D8       |
| WagonOutfits        | 0xDB096B85       |
| TransferHorse       | 0x4BC9DABB       |
| SellHorse           | 0xFF8109D8       |
| ActiveIt            | 0xC7B5340A       |
| CustomIt            | 0x760A9C6F       |
| CallWagon           | 0xF3830D8E       |
| CallHorse           | 0x24978A28       |
| MarketWithdraw      | 0x760A9C6F       |
| MarketBuy           | 0xC7B5340A       |
| SellMarket          | 0x9959A6F0       |

***

### Horse Equipment & Appearance

#### `ExtraEquip`

Defines extra cosmetic or functional items that can be added to horses. Each entry includes:

* `Hash`: Drawable hash of the item.
* `Stash`: Optional, defines how many extra inventory slots the equipment provides.
* `Flame`: Optional, for effects like flaming hooves.

You can freely add custom items by copying the format.

***

### Horse Behavior Settings

* `UseDefaultStats`: If `true`, uses default stats. If `false`, uses custom stats from `horses.lua`.
* `HorseEquipmentsWithGold`: Sets the payment type for horse equipment (gold or money).
* `TimeToDrink`, `DrinkAddHealth`, `DrinkAddStamina`: Controls drinking time and effects.
* `AttackEnemies`: If set to EXP value (e.g., 3500), horse can attack enemies when called.
* `StandbySit`: Time (in seconds) before idle horses lie down. `false` disables.

#### Visibility

* `HideNameHorseToOthers`: If `true`, only shows horse ID to others.
* `ShowCustomNameToOthers`: Shows custom label instead of name or ID.

#### Ownership

* `MaxHorses`: Max horses for normal players.
* `TrainersMaxHorses`: Max horses for horse trainers.
* `ByPassLimit`: Allows certain groups (VIP tiers) to own more horses.

***

### Horse Management

* `BuyHorseAge`: Age range for newly bought horses.
* `CallHorseOnlyInCities`, `SendHorseOnlyInCities`: Restrict horse summoning/sending to cities.
* `ReCallCooldown`, `ReSendCooldown`: Cooldowns for calling/sending horses.
* `ChanceSendAway`: % chance to send away unknown/agitated horses.
* `CallDistanceToRoads`: Distance (in meters) to roads for wagon spawn check.
* `LassoHorse`: Enable/disable horse lassoing.
* `ReviveItem`: Item required to revive a horse.
* `ChangeToSearchBags`: % chance the horse fails when searching bags.

#### Market

* `HorseSellPrice`: % of the original value when selling a horse.
* `BlacklistCities`: Cities where market actions are blocked.
* `TransferHorseBlacklist`, `SellHorseBlacklist`, `SellMarketHorseBlacklist`: Specific breeds blocked from actions.

***

### Horse Tricks

* `HorseTricksKey`: Key used to open the tricks menu.
* `HorseTricksCommand`: Command to open tricks menu or `false` to disable.
* `HorseTrickDistance`: Max distance for trick commands.
* `HorseTricks`: List of available tricks, each includes:
  * `Tittle`: Trick name
  * `Anim`, `Dict`: Animation and dictionary
  * `Time`: Duration in ms or `-1` for loop
  * `Flag`: 0 = no loop, 1 = loop
  * `Exp`: Experience reward

***

### Horse Theft & Recovery

#### Abandoned Stable for Stolen Horses

* `HidenStoledHorsesBlip`: Blip hash used to mark the abandoned stable on the map.
* `HidenStoledHorses`: Coordinates for the abandoned stable. Use `false` to disable.
* `HidenStoledHorsesName`: Name displayed on the map for the abandoned stable.
* `HorsesBlacklist`: List of horse models considered high value or special; they are excluded from theft-related actions.

***

### Feeding Horses

#### `Feed`

Defines consumable items for horses, including:

* `label`: Display name of the item.
* `boost`: Set to `true` if it applies full health/stamina instantly.
* `health`: Health restored.
* `stamina`: Stamina restored.
* `thirsty`: Thirst restored.
* `hungry`: Hunger restored.

Use `false` to disable specific effects (e.g., only restore stamina, not health).

***

### Wagon System Settings

* `WagonEquipmentsWithGold`: Choose payment type (gold or money).
* `WagonLowHealth`: Threshold below which wagons are undrivable.
* `ActiveLastPosition`: Allows calling/sending wagons only from last known position.
* `EnableOutfits`: Trigger to open outfits menu. Use `false` to disable.
* `SSHousing` / `SSClan`: Enables integration with SS-Housing / SS-Clan.
* `HammerRepair`: Item needed to repair wagons.
* `HammerRepairAnimation` / `HammerRepairScenario`: Set animation or scenario for repair.
* `HammerRepairTime`: Time (ms) required to repair a wagon.
* `HammerAddWagonHealth`: Health restored per repair.
* `HammerRepairNeeds`: Required items and amounts for repairs.

#### Restrictions

* `CallWagonOnlyInCities`, `SendWagonOnlyInCities`: Restrict wagon interactions to cities.
* `WagonDistanceToRoads`: Distance used to find road for wagon spawn.
* `MaxDistanceToCall`: Max range to call your wagon before respawn.

#### Market

* `MaxMarketPrice`: Maximum multiplier for horse price at market.
* `WagonSellPrice`: % value when selling a wagon.
* `BlackListCityLockpick`: Cities where wagon lockpicking is disabled.
* `TransferWagonBlacklist` / `SellWagonBlacklist`: List of wagons excluded from these actions.

***

### Horse Training System

#### `Experience`

Defines how stamina is affected based on EXP level:

* Higher EXP = faster regeneration and slower stamina loss.

#### `Training`

* `TrainerBookItem`: Item used to access all horses for trainers.
* `Jobs`: Jobs allowed to train horses.
* `ShoesTime`: Time for shoeing animation.
* `Whip`: Item used to begin training.
* `MinStamina`: Minimum stamina needed to train.

#### `ChoiceTraining`

* Set to `true` to let trainers choose the training type with the whip.

#### `HorseTraining`

**Type 1 - Step Training**

* Configured per stable with defined coordinates, EXP reward, and marker colors.

**Type 2 - Random Action Training**

* Random sequence of actions: jump, run, walk, etc.
* `StepsTime`: Time between actions.
* `StepsNeed`: Number of steps to complete.
* EXP granted for each successful action.

**Type 3 - Free Training**

* Passive EXP based on walking/running/skidding/rearing.

***

### Horseshoe System

#### `Shoes`

Each horseshoe type has a durability (`km`) and label. Losing shoes reduces stamina:

* `ironhorseshoe`: 20,000 km
* `silverhorseshoe`: 40,000 km
* `goldhorseshoe`: 80,000 km

***

### Horse Breeding System

#### `Breeding`

* `Jobs`: Allowed jobs.
* `AllowCross`: If `true`, enables special appearances.
* `Pill`: Item used by males to start breeding.
* `Brush`: Item to clean horses.
* `Chance`: % chance to start breeding.
* `BreedTime`: Animation time in ms.
* `ChanceFoal`: Chance for foal to inherit father’s breed.
* `ChanceSex`: Male/female ratio chance.
* `BreedWaitTime`: Days until birth.
* `Handicap`: Reduced stats for pregnant females.
* `CheckBreed`: How often (hours) breeding progress is checked.
* `StartRiding`, `StartBreeding`, `StartTraining`, `StartAdult`: Milestones for foal development.
* `StartOld`, `StartDead`, `StartDeleteIt`: Age-related transitions.
* `StopBreeding`: Max age to allow breeding.
* `EnableBlackLists`: Enable category-based breeding restrictions.

#### Breeding Categories

Breeding is only allowed within the same category. Each category includes specific horse breeds. If not listed, horses can't breed.

***

### Horse Taming System

#### `Taming`

* `Jobs`: Allowed jobs (includes civilian and many roleplay jobs).
* `MaxFails`: Max button fails before being thrown off.
* `MaxSucces`: Required correct presses to tame the horse.
* `RandomTime`: Time range (ms) to show the key prompt.
* `ReactionTime`: Time allowed to press key.
* `TamingPrice`: % of base horse price needed to tame.
* `SellPrice`: % value when taming and selling horse.
* `TamingAge`: Age range of horses that can be tamed.

***

### Stable Configuration

#### Global Stable Settings

* `TrainBreedZoneBlip`: Blip icon for training/breeding zone.
* `TrainBreedZoneName`: Label for the zone.

#### `Stables`

Each stable entry contains:

* `Name`: City/stable name
* `CamPos`: Camera position for UI
* `Blip`: Blip icon for map
* `MySpot`: Where horses are spawned
* `MyWagonSpot`: Where wagons are spawned
* `ActiveMyWagon`: Enable wagon functionality
* `CustomPos`: Optional interaction zone
* `TrainingType`: Type of training (1/2/3)
* `TrainingPos`: Position of training zone
* `Distance`: Max distance for stable interaction
* `SellHorses`, `SellWagons`, `SellPlayersHorse`: Market options
* `SellSpots`, `SellWagonsSpot`, `SellPlayersHorseSpot`: Sell positions

You can add or remove stables by copying one of the existing structures.

***

### Notifications

```lua
function NOTIFY(text)
  local VORPCore = exports.vorp_core:GetCore()
  VORPCore.NotifyLeft(Config.Texts["tittle_notification"], text, "generic_textures", "tick", 5000, "COLOR_WHITE")
end
```

Replace this with your own custom notify system if needed.

***
