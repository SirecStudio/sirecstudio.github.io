# SS-Telegram V4.4

## Update Summary

SS-Telegram V4.4 expands the telegram system with improved documentation, identity integration notes, anonymous telegram support, money transfer guidance, coordinate sharing, saved telegram items, and clearer setup instructions for server owners.

***

## Added

* Added full GitBook documentation for installation, configuration, usage, SQL, and troubleshooting.
* Added documentation for normal and anonymous telegram items.
* Added documentation for money transfer through telegrams.
* Added documentation for coordinate sharing and the required `coords` database column.
* Added documentation for saved telegram items and metadata usage.
* Added documentation for `SS-IdentityCard` integration.
* Added documentation for official job/institution sender names.

***

## Telegram System

* Documented the bird delivery flow for new telegrams.
* Documented unread telegram checks through `TimeCheck`.
* Documented stuck/dead bird reset through `ResetTelegram`.
* Documented normal bird and anonymous bird model configuration.

***

## Config & Translations

* Documented `config.lua`, `l/l.lua`, and `config.js`.
* Added setup notes for `EN`, `IT`, `ES`, `FR`, `DE`, `PT`, `RU`, and `RO`.
* Added safe configuration examples for items, webhooks, date, camera, money, and timers.

***

## SQL & Compatibility

* Documented VORP and RSG SQL files.
* Added upgrade note for the `coords` column required by coordinate sharing.

***

## Preview

* Added GitBook preview images for normal telegram, anonymous telegram, and telegram item visuals.
