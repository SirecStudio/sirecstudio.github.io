# Configuration Helps

## SS-Telegram Setup & Configuration Guide

SS-Telegram is an immersive RedM telegram system with bird delivery, normal and anonymous telegrams, saved telegram items, money transfer, coordinate sharing, address book support, Discord webhook logs, and optional `SS-IdentityCard` integration.

This guide is written for server owners who want to install, configure, and test the script safely.

***

## Features Overview

SS-Telegram includes:

* Normal telegram item flow.
* Anonymous telegram item flow.
* Bird delivery for new telegrams.
* Saved telegram items with metadata.
* Money transfer through telegrams.
* Coordinate sharing with temporary map blip and GPS route.
* Address book / saved receiver list.
* Optional `SS-IdentityCard` integration.
* Official job/institution sender names.
* Discord webhook logging.
* Multi-language support.

***

## Dependencies

### Required

* `SS-Core`
* `ghmattimysql`

### Optional Integrations

* `SS-IdentityCard`

If `SSIdentityCard = true`, start `SS-IdentityCard` before `SS-Telegram`.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-Telegram
```

Keep the resource folder name exactly:

```text
SS-Telegram
```

### 2. Import SQL

For VORP style character IDs, import:

```text
EXTRA/ss_telegram.sql
```

For RSG style character IDs, import:

```text
EXTRA/ss_telegram_rsg.sql
```

The main tables are:

```text
ss_telegram
ss_telegramlist
```

### 3. Check Coordinates Column

The current script supports coordinate sharing and writes a `coords` field to `ss_telegram`.

If your SQL table does not include `coords`, run:

```sql
ALTER TABLE `ss_telegram`
ADD COLUMN `coords` varchar(500) DEFAULT NULL;
```

### 4. Start Order

Recommended start order:

```cfg
ensure ghmattimysql
ensure SS-Core
ensure SS-IdentityCard
ensure SS-Telegram
```

If `SSIdentityCard = false`, `SS-IdentityCard` is not required.

### 5. Restart The Server

After importing SQL and checking the start order, restart the server and test normal telegrams, anonymous telegrams, money transfer, and coordinate sharing.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main configuration.
* `l/l.lua`: Lua translations.
* `config.js`: UI translations.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Telegram UI.
* `EXTRA/ss_telegram.sql`: VORP SQL.
* `EXTRA/ss_telegram_rsg.sql`: RSG SQL.

***

## Languages

Languages are configured in:

```text
config.lua
```

Example:

```lua
Language = "RO"
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

Lua translations are stored in:

```text
l/l.lua
```

NUI translations are stored in:

```text
config.js
```

***

## First Configuration

Open:

```text
config.lua
```

Start with:

```lua
Dev = true
Language = "EN"
Key = 0xD9D0E1C0
```

* `Dev`: Use `true` while testing, then set it to `false` on live servers.
* `Language`: Main script language.
* `Key`: Prompt key used for telegram interactions.

***

## SS-IdentityCard Integration

```lua
SSIdentityCard = true
OfficialJobs = {"police", "PolitiaFederala"}
```

When enabled, SS-Telegram can use:

* Real identity card names.
* Fake identity card names.
* Official job/institution sender names.
* Recipient search through identity card data.

If your server does not use SS-IdentityCard, disable it:

```lua
SSIdentityCard = false
```

***

## Telegram Items

```lua
Telegram = "telegram"
AnonymousTelegram = "blacktelegram"
UnlimitedTelegram = false
```

* `Telegram`: Item used to send normal telegrams.
* `AnonymousTelegram`: Item used to send anonymous telegrams.
* `UnlimitedTelegram`: Controls whether the item is consumed after sending.

If `UnlimitedTelegram = false`, one item is removed after a telegram is sent.

***

## Money Transfer

```lua
MaxMoneyAmount = 500
```

Players can send money through normal telegrams up to the configured maximum amount.

Recommended:

* Keep the max amount reasonable.
* Test with one player sending and another receiving.
* Confirm the money is removed from the sender and given to the receiver only once.

***

## Coordinate Sharing

The telegram UI can send the player's current coordinates.

When coordinates are included:

* The server stores them in the `coords` column.
* The receiver sees a location reference.
* A temporary map blip is created.
* A GPS route points to the shared location.
* Reading the saved telegram item later can show the location again.

Make sure the database includes:

```sql
ALTER TABLE `ss_telegram`
ADD COLUMN `coords` varchar(500) DEFAULT NULL;
```

***

## Bird Delivery

Bird settings:

```lua
Model = "A_C_Eagle_01"
ModelAnonymouse = "a_c_crow_01"
Use3DCam = false
CameraKey = 0x4BC9DABB
```

* `Model`: Bird used for normal telegrams.
* `ModelAnonymouse`: Bird used for anonymous telegrams.
* `Use3DCam`: Enables optional camera mode.
* `CameraKey`: Key for the optional camera mode.

Players must be in a valid outdoor situation before calling the telegram bird down.

***

## Timers

```lua
TimeCheck = 60
ResetTelegram = 600
```

* `TimeCheck`: How often the script checks for unread telegrams.
* `ResetTelegram`: Failsafe timer for stuck/dead bird delivery.

Use `false` to disable the reset:

```lua
ResetTelegram = false
```

***

## Webhook Logs

```lua
Webhook = ""
WebhookTittle = "NEW TELEGRAM HAS BEEN SENT"
```

Leave `Webhook` empty to disable Discord logs.

If enabled, use a private staff log channel because telegram logs may contain roleplay information.

***

## Normal Telegram Flow

1. Player uses the normal telegram item.
2. Bird spawns and flies to the player.
3. Player opens the telegram UI.
4. Player selects sender identity, receiver name, message, optional money, and optional coordinates.
5. Server finds the receiver.
6. Server inserts the telegram in `ss_telegram`.
7. Item and money are removed according to config.

***

## Anonymous Telegram Flow

1. Player uses the anonymous telegram item.
2. Bird spawns and flies to the player.
3. Player writes the telegram.
4. Sender name is saved as anonymous.
5. Receiver can read the telegram without seeing the sender's identity.

***

## Receiving Telegrams

1. Client checks for unread telegrams every `TimeCheck` seconds.
2. Player receives a notification when a telegram exists.
3. Bird delivery starts.
4. Player calls the bird down.
5. Player reads the telegram.
6. Telegram is saved as an inventory item with metadata.
7. Database row is marked as read.

***

## Saved Telegrams

After reading a new telegram, the player receives a saved telegram item.

Saved telegrams can be:

* Read again later.
* Dropped.
* Given to another player.
* Used as roleplay evidence.

***

## Troubleshooting

### The Bird Does Not Come

Check:

* Item names in `config.lua`.
* `SS-Core` usable item registration.
* Player is outside.
* Player is not mounted, tied, dead, or inside a vehicle.
* `ResetTelegram` is not blocking a stuck delivery for too long.

### Recipient Is Not Found

Check:

* First name and last name spelling.
* `SSIdentityCard` setting.
* `SS-IdentityCard` data if integration is enabled.
* Framework character table data if integration is disabled.

### Money Cannot Be Sent

Check:

* `MaxMoneyAmount`.
* Player has enough money.
* Money value is a valid whole number.
* `SS-Core` money functions work on your server.

### Coordinates Do Not Save

Check:

* `coords` column exists in `ss_telegram`.
* Server console for SQL insert errors.
* The player selected the coordinate option in the telegram UI.

### Old Telegram Item Does Not Open

Check:

* Item metadata contains `id`.
* `SS-Core` registered usable items.
* The database row still exists.

### UI Opens In The Wrong Language

Check:

* `Language` in `config.lua`.
* Language key exists in `l/l.lua`.
* UI text exists in `config.js`.
* Resource was restarted after config changes.

***

## Recommended Live Checklist

Before going live, confirm:

* SQL has been imported.
* `coords` column exists if coordinate sharing is used.
* `ghmattimysql` starts before `SS-Telegram`.
* `SS-Core` starts before `SS-Telegram`.
* `SS-IdentityCard` starts before `SS-Telegram` if enabled.
* `Dev = false`.
* Language is selected.
* Normal telegram item works.
* Anonymous telegram item works.
* New telegram delivery works.
* Saved telegram item opens.
* Money transfer works.
* Coordinate sharing works.
* Webhook is tested or left empty.
