# SS-Stable V4.6

## New Features

* Added a new stamina experience control system. Horse stamina depletion and regeneration can now be adjusted with custom multipliers based on XP levels: under 1000 XP, over 1000 XP, over 2000 XP, over 3000 XP, and 4000 XP.
* Added 28 new custom horse coats, bringing the total number of custom coats to 54.
* Added horse tricks, which can be activated by command, by key, or by both. The default key behavior is triggered when the horse is locked and the player presses B.
* Added support for custom experience requirements on horse tricks, allowing each trick to require a specific XP level.
* Added SS-Admin functions. More details are available in the SS-Admin update.

***

## Fixes

* Fixed wagon repair so it correctly restores the entire wagon, including missing wheels.
* Fixed an issue where owned horse prices changed when scrolling through the owned horses list.

***

## Improvements

* Reworked the horse synchronization system. The old `-1` method, which synced to all players, caused major server overflow when calling or sending horses. It has been replaced with a new optimized sync system designed to prevent overflow.
* Optimized market refresh behavior. The market no longer auto-refreshes and now updates only when a player searches for horses near the market area, reducing unnecessary Client > Server and Server > Client data flow.
* Reorganized the config file and added more detailed explanations, making the setup easier to understand for both server owners and new customers.

***

## Changes

* Moved all translation strings out of `config.lua` into `translate/translate.lua`, keeping the configuration cleaner and more modular.
* Updated extra equipment support. A horse can now use up to 3 extra equipment items at the same time, such as extra stash, flaming horseshoes, and torch.
* Removed full wagon repair with wheels from SS-Stable. That repair flow now belongs to SS-WheelWright. SS-Stable keeps the hammer repair system, with configurable health amount, scenario, animation, required items, and item amount.
* Added a configurable maximum horse market price multiplier. This prevents players from listing horses at extremely high prices and leaving them on the market indefinitely.

***

## Preview

![](../../.gitbook/assets/IMG_0073.png)![](../../.gitbook/assets/IMG_0058.png)

<figure><img src="../../.gitbook/assets/Screenshot_2024-11-22_203653.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot_2024-11-23_141937.png" alt=""><figcaption></figcaption></figure>
