# SS-Admin V4.7

## Update Summary

SS-Admin V4.7 introduces a more complete administration workflow with panel-based staff tools, expanded permissions, ticket handling, admin chat, admin jail persistence, moderation actions, and improved configuration documentation.

***

## Added

* Added full GitBook documentation for setup, configuration, permissions, ticket system, admin chat, admin jail, and troubleshooting.
* Added admin panel documentation covering player tools, moderation actions, economy actions, horse tools, wagon tools, and staff utilities.
* Added documentation for Discord role permissions and Steam identifier permissions.
* Added documentation for Discord whitelist setup.
* Added documentation for SQL import and database usage.
* Added documentation for `ReportList` and `Report` exports.

***

## Admin Panel & Permissions

* Documented the NUI admin panel workflow.
* Documented important permission indexes and how to safely restrict actions by role.
* Documented command-based and panel-based action access.
* Documented admin categories: `ADMIN`, `MODERATOR`, and `HELPER`.

***

## Ticket & Staff Systems

* Documented the player report command.
* Documented ticket statuses and staff handling flow.
* Documented admin chat behavior and history limit.
* Documented admin jail position, radius, release position, and database persistence.

***

## Config & Translations

* Documented `config.lua`, `s/config.lua`, `l/l.lua`, and `config.js`.
* Added setup notes for `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, and `PT`.
* Added safe editing rules for server owners.

***

## Stability & Setup

* Added recommended start order for `oxmysql`, `SS-Core`, and `SS-Admin`.
* Added optional `pma-voice` setup notes for admin voice.
* Added troubleshooting for permissions, whitelist, Discord bot setup, ticket logs, admin voice, and startup issues.
