# SS-Stable V4.7

## Update Summary

This update focuses on important bug fixes, stability improvements, optimization, and cleaner configuration across multiple SS-Stable systems.

***

## Fixes & Improvements

* Optimized the horse and wagon preview system.
* Fixed incorrect stats displayed in the UI for market, my horses, and preview screens.
* Fixed horse equipment visually disappearing when switching categories in the shop or stable.
* Fixed crossbreed visuals so they are applied correctly in preview, my horse preview, and called horses.
* Fixed the horseshoe system so the item is reserved and consumed correctly, preventing duplication through fast transfers.
* Fixed animal quality when animals are placed into or removed from wagons, keeping the correct star quality.
* Fixed wagon repair so it starts directly when using the repair item near the wagon, without spawning an extra hammer prop.

***

## Added

* Added wagon blocking when the wagon is too damaged, configurable through `BlockWagonIfDamage`.
* Wagon stash, cargo, outfits, and tarpaulin actions are now blocked when the wagon is too damaged.

***

## Horse Equipment System

* Added a new system for the `horseequipment` item.
* Players can remove the main equipment from a personal horse and save it as item metadata.
* Players can apply saved equipment to another personal horse.
* The system works only inside stable zones.
* Mane, tail, mustache, and extra equipment are not included.
* Equipment cannot be applied to a horse that already has main equipment.
* Fixed `bags` updates after removing or applying horse equipment.
* Search bags and inventory now update correctly without needing to send away and recall the horse.

***

## Config & Translations

* Reorganized and documented `config.lua` and the files inside `cfg` more clearly.
* Grouped settings more logically by system, including general, horse, wagon, and related sections.
* Added and fixed missing translations.
* Removed extra or unused translations where needed.
* Prepared translations in the same style as SS-IdentityCard for `EN`, `IT`, `ES`, `FR`, `DE`, `PT`, `RU`, and `RO`.

***

## Stability & Performance

* Reduced the risk of runtime issues.
* Improved idle/active wait logic for prompts and UI behavior.
* Added more defensive checks for entities, models, metadata, and native calls.
