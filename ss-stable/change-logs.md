# Change logs

### 01/04/2025

* The synchronization system for horses has been reworked. The old method using -1 (sync to all players) caused major server overflow when calling or sending horses. This has now been replaced with a new, optimized sync system with zero overflow. If this new system proves stable, it will also be applied to wagons, improving overall performance.
* FIXED (Repair Wagon)- Wagon repair now correctly restores the entire wagon, including any missing wheels.
* FIXED (Price of own horses)- Fixed a bug where horse prices would change every time you scrolled through your owned horses.
* ADDED (Stamina Experience Control)- A new stamina control system based on experience has been added. You can now set custom stamina depletion and regeneration multipliers based on horse XP levels: Under 1000 XP, Over 1000 XP, Over 2000 XP, Over 3000 XP , 4000 XP !
* ADDED ( Horse Coats )- 28 new custom horse coats have been added. Total all custom coats available: 54
* OPTIMIZED (Market Refresh)- The market no longer auto-refreshes, which previously caused data overflow (Client > Server, Server > Client). Now, the list refreshes only when a player searches for horses near the market area.
* CHANGED ( Translated texts )- All translation strings have been moved out of the config.lua file (which was getting too large). They are now located in translate/translate.lua, making configuration more modular and easier to manage.
* UPDATED ( Extra Equip )- You can now equip up to 3 extra equipment items on the same horse, such as: Extra stash, Flaming horseshoes, Torch

![](../.gitbook/assets/IMG_0073.png)![](../.gitbook/assets/IMG_0058.png)

### **29/11/2024**

* Has been added the horse tricks, wich you can active it by command, or by key (default is when you lock the horse and press B ) , you can add more tricks with experience needed to do that trick. Allow command, key or both !
* Many reports that people add their horses in market with an high price, and they remain there for eternity :) . Now you can set the max market price by X 2...3.. of the horse price !
* Has been removed the REPAIR with wheels etc etc, now will remain only on SS-WheelWright. Stable has only repair with hammer adding amount of health for every repair, scenario, animation, items need and amount can be set from config.
* Has been added functions for SS-Admin ! ( Read on SS-Admin Update )
* The config file has been re-organized and added more details about everything, so you or new customers can understand everything since Stable has many functions !
*

    <figure><img src="../.gitbook/assets/Screenshot_2024-11-22_203653.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/Screenshot_2024-11-23_141937.png" alt=""><figcaption></figcaption></figure>

