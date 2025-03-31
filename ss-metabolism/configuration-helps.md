# Configuration Helps

***

### General Settings

* **Dev Mode**: `Dev = true` - Enables debug mode for testing; set to `false` for production.
* **Set HUD Command**: `CommandSetHud = "sethud"` - Allows players to move and save HUD icon positions with `ESC`.
* **Toggle HUD Command**: `ToggleHud = "shud"` - Shows or hides the metabolism HUD.
* **Refresh Rate**: `Refresh = 20` - The interval (in seconds) at which metabolism stats like hunger, thirst, stress, and dirtiness are updated. Recommended value: **10-20**.

***

### Initial Metabolism Values:

When a player joins the server, their metabolism stats start with:

* **Thirst**: `90`
* **Hunger**: `75`
* **Stress**: `10`
* **Reputation**: `500`

***

### System Features:

* **Health & Stamina Tracking**:
  * `UseHealthStamina = false` - Disables health & stamina tracking.
  * `UseHorseHealthStamina = true` - Enables horse health & stamina tracking.
* **Reputation System**:
  * `RepStats = true` - Enables reputation tracking.
  * `ActiveNpcHate = true` - NPCs react based on reputation.
  * **Reputation Thresholds**:
    * `PeopleStartWalkingAway = 3` - NPCs start walking away at low reputation.
    * `PeopleStartRunningAway = 2` - NPCs start running away at very low reputation.
    * `PeopleStartHateYou = 1` - NPCs attack when reputation is critically low.
  * **NPC Blacklist**: `BlackListModels` - Defines NPC models that ignore reputation actions.

***

### Horse Metabolism:

* **Horse Metabolism Decay**:
  * `HorseStats = true` - Enables horse metabolism tracking.
  * `HorseMetabolism = {Thirsty = 1, Hungry = 1}` - Defines how quickly a horse's hunger & thirst decrease every refresh tick.

***

### Temperature System:

* **Temperature Range**: `Temperature = {3, 35}` - Defines the min/max temperature in the game.
* **Temperature Effects on Metabolism**:
  * `TemperatureSettings["MIN"]` - Effects when temperature is below **minimum**:
    * `Thirsty = 0`
    * `Hungry = 0.5`
    * `Stress = 0.2`
  * `TemperatureSettings["MAX"]` - Effects when temperature is above **maximum**:
    * `Thirsty = 0.5`
    * `Hungry = 0`
    * `Stress = 0.2`

***

### Metabolism Changes by Activity:

* `Idle`: `Thirsty = 0.4, Hungry = 0.3, Stress = 0`
* `Walking`: `Thirsty = 0.7, Hungry = 0.6, Stress = 0`
* `Running`: `Thirsty = 1.0, Hungry = 0.8, Stress = 0`
* `Combat`: `Thirsty = 1.2, Hungry = 1.2, Stress = 5`
* `In Boat`: `Thirsty = 0.5, Hungry = 0.4, Stress = -5`
* `In Wagon`: `Thirsty = 0.5, Hungry = 0.4, Stress = -3`
* `On Mount`: `Thirsty = 0.4, Hungry = 0.4, Stress = -1`

***

### Health Effects:

* `KillWhenZero = false` - Determines if a player should die when hunger or thirst reaches 0.
* `DecreaseByStress = 0.2` - Defines how much stress affects hunger & thirst as a percentage.
* **Minimum Metabolism Values**:
  * `MetabolismMin = 20` - The lowest metabolism threshold before penalties apply.
  * **Penalties for Low Stats**:
    * `THIRSTY`: `Health = 30, Stamina = 10, Stress = 5`
    * `HUNGRY`: `Health = 25, Stamina = 5, Stress = 5`

***

### Stress System:

* `StressRagdoll = true` - Enables ragdoll effect due to stress.
* `RagDollObjects = true` - Players ragdoll when running into objects (chance: 85%).
* `RagDollFalling = false` - Disables ragdoll when falling.
* **Stamina Depletion Under Stress**:
  * `DecreaseFasterStamina1 = 1.5` - Stamina decreases faster when stress is **50%**.
  * `DecreaseFasterStamina2 = 2.0` - Stamina decreases faster when stress is **80%**.

***

### Exports (For Developers):

These exports allow other scripts to interact with SS-Metabolism:

* **Stress Management**:
  * `exports["SS-Metabolism"]:GetStress()`
  * `exports["SS-Metabolism"]:AddStress(AMOUNT)`
  * `exports["SS-Metabolism"]:RemoveStress(AMOUNT)`
* **Thirst Management**:
  * `exports["SS-Metabolism"]:GetThirsty()`
  * `exports["SS-Metabolism"]:AddThirsty(AMOUNT)`
  * `exports["SS-Metabolism"]:RemoveThirsty(AMOUNT)`
* **Hunger Management**:
  * `exports["SS-Metabolism"]:GetHungry()`
  * `exports["SS-Metabolism"]:AddHungry(AMOUNT)`
  * `exports["SS-Metabolism"]:RemoveHungry(AMOUNT)`
* **Reputation Management**:
  * `exports["SS-Metabolism"]:GetRep()`
  * `exports["SS-Metabolism"]:AddRep(AMOUNT)`
  * `exports["SS-Metabolism"]:RemoveRep(AMOUNT)`
* **Horse Metabolism**:
  * `exports["SS-Metabolism"]:GetHorseHungry()`
  * `exports["SS-Metabolism"]:AddHorseHungry(AMOUNT)`
  * `exports["SS-Metabolism"]:RemoveHorseHungry(AMOUNT)`
  * `exports["SS-Metabolism"]:GetHorseThirsty()`
  * `exports["SS-Metabolism"]:AddHorseThirsty(AMOUNT)`
  * `exports["SS-Metabolism"]:RemoveHorseThirsty(AMOUNT)`

***

### Notifications:

* `NOTIFY(text)` - Calls a notification with `TriggerEvent("vorp:TipBottom", text, 5000)`.

This guide provides an overview of all configurable options for **SS-Metabolism**, allowing you to fine-tune the system based on your server’s needs.
