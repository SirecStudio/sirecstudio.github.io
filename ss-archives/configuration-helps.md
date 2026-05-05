# Configuration Helps

## SS-Archives Setup & Configuration Guide

SS-Archives is a police archive system for RedM. It supports citizen search, dossier management, jail/prison logic, property and store seizure, officer notes, webhook logs, and integration with SS-IdentityCard.

This guide is written for server owners who want to install, configure, and test the script safely, even without deep Lua knowledge.

***

## Features Overview

SS-Archives includes:

* Sheriff archive UI for allowed police/government jobs.
* Citizen search and identity record access.
* Dossier creation with fine, jail, work, bounty, and penal status.
* Dossier deletion with grade restrictions.
* Archive notes on citizens.
* Identity card creation from the archive through `SS-IdentityCard`.
* Automatic jail and manual jail flows.
* Prison canteen, prison work, and sentence reduction while online.
* Property and store seizure/unseizure support.
* Internal officer notes board stored in server memory.
* Webhook logs for important archive actions.

***

## Dependencies

### Required

* `SS-Core`
* `ghmattimysql`
* `menuapi`
* `PolyZone`
* `SS-IdentityCard`

### Used By Default

* `vorp:TipBottom`, used for notifications.

### Optional Integrations

* `SS-Housing`
* `SS-PlayerShops`
* `SS-BountyHunter`

If you do not use an optional integration, disable it in `config.lua`.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-Archives
```

Keep the resource folder name exactly:

```text
SS-Archives
```

### 2. Import SQL

Import the main archive SQL file:

```text
EXTRA/sql.sql
```

Optional or update SQL files:

```text
EXTRA/sql-notes.sql
EXTRA/sql-work-update.sql
```

Main tables used by this script:

* `ss_archives`
* `ss_archivesnotes`

Also used through integrations:

* `ss_identitycard`
* `ss_housing`
* `ss_playershops`

### 3. Start Order

Recommended start order:

```cfg
ensure ghmattimysql
ensure SS-Core
ensure SS-IdentityCard
ensure SS-Archives
```

If you use property, store, or bounty integrations, make sure those resources also start before or together with `SS-Archives`.

### 4. Restart The Server

After importing SQL and checking the start order, restart the server and test the archive flow in-game.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main configuration.
* `l/l.lua`: Server/client translations.
* `config.js`: Archive UI texts.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Archive UI page.

***

## Languages

Languages are configured in:

```text
l/l.lua
```

Included languages:

* `EN`
* `IT`
* `ES`
* `FR`
* `DE`
* `PT`
* `RU`
* `RO`

Example:

```lua
Language = "RO"
```

If an invalid language is set, the script falls back to `EN`.

Important:

* `l/l.lua` controls game-side notifications and messages.
* `config.js` controls UI text shown inside the archive page.

***

## First Configuration

Open:

```text
config.lua
```

The file is grouped into clear sections so you can change values without touching logic.

### General Settings

```lua
Dev = true
Language = "EN"
WebHook = ""
Key = 0xD9D0E1C0
Align = "right"
ServerYear = "1905"
```

* `Dev`: Use `true` while testing. Use `false` on live servers.
* `Language`: Translation language used by the script.
* `WebHook`: Discord webhook URL for archive action logs.
* `Key`: Interaction key used by menu prompts.
* `Align`: Menu alignment.
* `ServerYear`: Lore/server year printed on archive records.

### Job & Permission Settings

```lua
AllowedJobs = {"Guvernator", "marshal", "sheriff", "police"}
OfficerNotesCooldown = 1
DeleteNotesGrade = 5
DeleteJobGrade = 9
SeizureProperty = 5
TransferProperty = 8
```

* `AllowedJobs`: Jobs allowed to open and use the archive.
* `OfficerNotesCooldown`: Minutes between each officer note.
* `DeleteNotesGrade`: Minimum grade required to remove archive notes.
* `DeleteJobGrade`: Minimum grade required to delete dossiers.
* `SeizureProperty`: Minimum grade required to seize/unseize properties and stores.
* `TransferProperty`: Minimum grade reserved for transfer-related logic.

### Items & Commands

```lua
NoteBook = "archivesbook"
DossierItem = "sulf"
ShowJailDossier = "showdossier"
HideJailDossier = "hidedossier"
```

* `NoteBook`: Usable inventory item that opens the archive UI.
* `DossierItem`: Item used for dossier copies.
* `ShowJailDossier`: Command used to show jail paper.
* `HideJailDossier`: Command used to hide jail paper.

***

## Archive Offices

Offices are configured in:

```lua
Config.Offices
```

Example:

```lua
[1] = {
    Name = "Blackwater Archive",
    Pos = {-761.92, -1266.88, 44.05, 170.40},
    Blip = 587827268,
    Distance = 2.0,
}
```

Important fields:

* `Name`: Office name used for prompt and blip.
* `Pos`: Coordinates in `x, y, z, heading` format.
* `Blip`: Blip hash or `false`.
* `Distance`: Interaction range.

### Add A New Archive Office

Copy an existing office and change only the values:

```lua
[2] = {
    Name = "Valentine Archive",
    Pos = {-180.00, 625.00, 114.00, 90.00},
    Blip = 587827268,
    Distance = 2.0,
}
```

After adding a new office, restart the resource/server and test the prompt, blip, archive opening, and permissions.

***

## Dossier Flow

Main flow:

1. Officer opens the archive.
2. Officer searches a citizen.
3. Officer opens that citizen file.
4. Officer selects `Add Dossier`.
5. Officer sets charge, jail, work, fine, bounty, description, and flags.
6. Script creates a dossier in `ss_archives`.
7. If auto jail is enabled and the player is online, the player can be jailed immediately.

Important:

* `jail` in the dossier remains the original sentence given by the officer.
* Remaining jail time is tracked separately in `jailtime`.
* Jail time does not continue while the player is offline.

***

## IdentityCard Integration

SS-Archives is connected to `SS-IdentityCard`.

It uses `SS-IdentityCard` to:

* Read citizen identity data.
* Read notes linked to identity.
* Create identity cards from the archive UI.
* Support fake/real identity checks when needed.

From the archive, officers can create an identity card for a player if that player does not already have one.

***

## Prison & Penitentiary Settings

The prison configuration is in:

```lua
Config.Penintetiary
```

This section controls:

* Prison polygon.
* Prison cells.
* Canteen.
* Prison NPCs.
* Job permit area.
* Boat transport for manual jail.
* Release position.

### Prison Work

The crop job configuration is in:

```lua
Config.CropJob
```

Example:

```lua
CropJob = {
    Name = "Work for the benefit of the Country",
    WorkBonus = 20,
    Money = false,
    WaitCrop = 10000,
}
```

* `WorkBonus`: Seconds reduced from sentence per completed crop.
* `Money`: `false` disables payment, or use a number.
* `WaitCrop`: Work duration before reward or reduction is applied.

***

## Property & Store Integrations

If enabled:

```lua
SSHousing = true
SSPlayerShops = true
```

The archive can:

* List houses.
* List stores.
* Seize and unseize them.

This script updates the database and local archive cache. It does not broadcast refreshes to all players.

***

## Officer Notes

The `Officer Notes` page replaces the old global dossier page.

Behavior:

* Available in the archive UI.
* Messages are kept only in server memory.
* Notes reset automatically when the resource/server restarts.
* Notes are synced only to players with jobs listed in `Config.AllowedJobs`.
* Cooldown is controlled by `OfficerNotesCooldown`.

***

## Webhook Logs

Set your Discord webhook here:

```lua
WebHook = "https://discord.com/api/webhooks/..."
```

Leave it empty to disable Discord logs.

The script sends logs for actions such as:

* Create dossier.
* Delete dossier.
* Seize/unseize store.
* Seize/unseize house.

***

## Notification Handler

You can replace the default notify function in `config.lua`:

```lua
function ARCHIVESNOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000)
end
```

If your server uses another notification system, change only this function.

***

## Fine / Billing Handler

You can replace the default fine destination in `config.lua`:

```lua
function ADDFINES(source, charid, amount, tittle, description)
    TriggerEvent("S!r@#Blu$$-SS-ARCHIVES:SERVER:SENDFINE", source, charid, amount)
end
```

If your billing system is different, change only this function.

***

## Example Config Recipes

### Disable Property Integration

```lua
SSHousing = false
SSPlayerShops = false
```

### Allow Only Sheriff And Marshal

```lua
AllowedJobs = {"marshal", "sheriff"}
```

### Make Officer Notes Slower

```lua
OfficerNotesCooldown = 2
```

This means one note every 2 minutes.

### Disable Auto Jail Choice

```lua
AutoJail = false
```

### Make Dossier Deletion Stricter

```lua
DeleteJobGrade = 12
```

***

## Troubleshooting

### Archive Opens But There Is No Citizen Data

Check:

* `SS-IdentityCard`.
* Callback integrations between both resources.
* SQL imported correctly.
* Resource start order.

### Dossier Is Created But Jail Does Not Start

Check:

* `AutoJail`.
* Player online status.
* Character ID integration.
* Prison config.

### Officer Notes Do Not Sync

Check:

* Player job is included in `AllowedJobs`.
* Resource started correctly.
* Client opened the archive after startup.

### Properties / Stores Do Not Show

Check:

* `SSHousing`.
* `SSPlayerShops`.
* Corresponding database tables.

### Notebook Item Does Nothing

Check:

* `NoteBook` item name.
* Usable item registration.
* `SS-Archives` resource started.

***

## Recommended Live Checklist

Before going live, confirm:

* SQL has been imported.
* `SS-Core` starts before `SS-Archives`.
* `SS-IdentityCard` starts before `SS-Archives`.
* `Dev = false`.
* `Language` is selected.
* Optional integrations are disabled if missing.
* Archive office works.
* Notebook item works.
* Citizen search works.
* Dossier create/delete works.
* Jail flow works.
* Officer notes work.
* Property/store actions work.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature.
* `false` disables a feature.
* Numbers do not use quotes: `100`.
* Item names usually use quotes: `"itemname"`.
* Coordinates usually look like `{x, y, z, heading}`.

Bad:

```lua
DeleteJobGrade = "9"
```

Good:

```lua
DeleteJobGrade = 9
```

