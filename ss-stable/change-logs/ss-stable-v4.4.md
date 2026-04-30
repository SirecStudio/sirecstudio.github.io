# SS-Stable V4.4

## Update Summary

This is an important update for SS-Stable. It fixes several known issues and improves synchronization, market behavior, stamina control, translations, equipment handling, and documentation.

Please read the changelog carefully before updating. If anything is unclear, ask for support before applying the update on a live server.

***

## Fixes & Improvements

* Reworked the horse synchronization system. The previous `-1` sync method, which synced to all players, could cause major server overflow when calling or sending horses. It has been replaced with a new optimized sync system designed to prevent overflow.
* Fixed wagon repair so it correctly restores the entire wagon, including missing wheels.
* Fixed an issue where owned horse prices changed every time players scrolled through their owned horses.
* Optimized market refresh behavior. The market no longer auto-refreshes and now updates only when a player searches for horses near the market area, reducing unnecessary Client > Server and Server > Client data flow.

***

## Added

* Added a new stamina experience control system. Horse stamina depletion and regeneration can now be adjusted with custom multipliers based on XP levels: under 1000 XP, over 1000 XP, over 2000 XP, over 3000 XP, and 4000 XP.
* Added 28 new custom horse coats, bringing the total number of custom coats to 54.
* Added full SS-Stable documentation.

***

## Changes

* Moved all translation strings out of `config.lua` into `translate/translate.lua`, making the configuration cleaner, smaller, and more modular.
* Updated extra equipment support. A horse can now use up to 3 extra equipment items at the same time, such as extra stash, flaming horseshoes, and torch.

***

## Documentation

Full documentation for SS-Stable is available here:

```text
https://docs.sirecstudio.com/ss-stable
```

If anything is missing or unclear, please report it so the documentation can be improved.
