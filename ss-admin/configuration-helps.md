# Configuration Helps

## SS-Admin Setup & Configuration Guide

SS-Admin is an advanced admin panel and staff toolset for RedM. It includes player moderation actions, ticket reports, admin chat, admin jail, Discord or Steam permissions, optional whitelist checks, server utility tools, economy tools, and integrations with other Sirec Studio systems.

This guide is written for server owners who want to install, configure, and test the script safely.

***

## Features Overview

SS-Admin includes:

* NUI admin panel with dashboard, player tools, tickets, ban list, item/weapon tools, horse tools, wagon tools, and admin chat.
* Staff actions such as revive, heal, freeze, kill, spectate, bring, goto, kick, warn, ban, unban, notify, cuff, and admin jail.
* Utility tools such as noclip, god mode, waypoint teleport, coordinate teleport, player blips, nearby player visibility, clear zone, and admin stash.
* Economy tools for giving money, gold, items, and weapons.
* Horse and wagon admin tools.
* Ticket system with player report command.
* Admin chat with configurable in-memory history.
* Discord role permissions or Steam identifier permissions.
* Optional Discord whitelist.
* Multi-language support for Lua and UI text.

***

## Dependencies

### Required

* `SS-Core`
* `oxmysql`

### Optional

* `pma-voice`, only if `AdminVoice = true`.

### Related Integrations

* `SS-Stable`, used by horse and wagon related admin actions.
* `SS-IdentityCard`, used by identity creation and identity removal actions.
* `SS-PoliceJob`, used by cuff metadata events if your server uses that integration.

If you do not use the related scripts, restrict or disable the matching permission buttons.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-Admin
```

Keep the resource folder name exactly:

```text
SS-Admin
```

### 2. Import SQL

Import:

```text
EXTRA/ss_admin.sql
```

This creates the table:

```text
ss_admin
```

The table stores player identifiers, warnings, ban state, ban details, playtime, last join/leave data, and admin jail time.

### 3. Start Order

Recommended start order:

```cfg
ensure oxmysql
ensure SS-Core
ensure SS-Admin
```

If admin voice is enabled:

```cfg
ensure pma-voice
```

### 4. Restart The Server

After importing SQL and configuring permissions, restart the server fully and test with one staff account before opening the server to players.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main script configuration.
* `s/config.lua`: Discord bot token and guild ID.
* `l/l.lua`: Lua translations.
* `config.js`: UI translations.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Admin panel UI.
* `EXTRA/ss_admin.sql`: SQL table.

***

## Languages

The main language is configured in:

```text
config.lua
```

Example:

```lua
Language = "EN"
```

Included languages:

* `EN`
* `RO`
* `IT`
* `DE`
* `FR`
* `ES`
* `PT`

Lua translations are in:

```text
l/l.lua
```

UI translations are in:

```text
config.js
```

***

## First Configuration

Open:

```text
config.lua
```

Start with the general settings:

```lua
Language = "EN"
AdminVoice = true
RoleplayNameList = false
OpenMenu = 0x3C3DD371
ActiveCommands = true
MaxWarns = 3
BanWarns = 3
Notify = true
```

* `Language`: Main language used by Lua notifications and supported UI text.
* `AdminVoice`: Sends staff to the admin voice channel when they have admin access.
* `RoleplayNameList`: Uses character names instead of Steam names in player lists and commands.
* `OpenMenu`: Key hash used to open the admin panel, or `false` to disable key opening.
* `ActiveCommands`: Enables admin commands such as `/kick`, `/ban`, `/tp`, `/givemoney`, and `/giveitem`.
* `MaxWarns`: Number of warnings before automatic ban.
* `BanWarns`: Number of days for the automatic ban.
* `Notify`: Sends notifications for admin actions.

***

## Discord Bot Setup

Open:

```text
s/config.lua
```

Set:

```lua
Discord = {
    Token = "YOUR_BOT_TOKEN",
    GuildId = "YOUR_DISCORD_SERVER_ID",
}
```

The Discord bot is required when:

* `UseSteamPermissions = false`
* Discord role permissions are used.
* Discord whitelist is enabled.

Keep the token private. Never share it publicly or include it in screenshots.

***

## Permission Mode

### Discord Permissions

Use this mode when staff access should be based on Discord role IDs:

```lua
UseSteamPermissions = false

DiscordPermissions = {
    {name = "ADMIN", roles = {"ROLE_ID_HERE"}},
    {name = "MODERATOR", roles = {"ROLE_ID_HERE"}},
    {name = "HELPER", roles = {"ROLE_ID_HERE"}},
}
```

The role names `ADMIN`, `MODERATOR`, and `HELPER` are then used inside `Permissions`.

### Steam Permissions

Use this mode when staff access should be based on Steam identifiers:

```lua
UseSteamPermissions = true

SteamPermissions = {
    {name = "ADMIN", roles = {"steam:xxxxxxxxxxxx"}},
    {name = "MODERATOR", roles = {}},
    {name = "HELPER", roles = {}},
}
```

***

## Whitelist

Whitelist is controlled by:

```lua
WhiteList = true
WhiteListRoles = {"DISCORD_ROLE_ID"}
```

If `WhiteList = true`, players must have one of the configured Discord roles to join.

If your server does not use SS-Admin for whitelist access, set:

```lua
WhiteList = false
```

***

## Admin Permissions

Admin permissions are configured in:

```lua
Permissions = {
    [1] = { Command = "adminmenu", Roles = {"ADMIN", "MODERATOR", "HELPER"} },
}
```

Each entry has:

* `Command`: Chat command used for that action, or `false` if it should only be used from the panel.
* `Roles`: Staff categories allowed to use the action.

Do not change the numeric indexes. The script logic depends on those numbers.

### Common Permission Examples

Only admins can ban:

```lua
[28] = { Command = "ban", Roles = {"ADMIN"} },
```

Admins and moderators can revive:

```lua
[17] = { Command = "revive", Roles = {"ADMIN", "MODERATOR"} },
```

Disable a command but keep the panel button:

```lua
[21] = { Command = false, Roles = {"ADMIN"} },
```

***

## Important Permission Indexes

* `[1]`: Open admin panel.
* `[2]`: Announce.
* `[3]`: Spawn wagon / horse menu.
* `[4]`: Noclip.
* `[5]`: Waypoint or coordinate teleport.
* `[11]`: Player blips.
* `[13]`: Unban.
* `[14]`: Spectate.
* `[17]`: Revive player.
* `[18]`: Heal player.
* `[19]`: Give money.
* `[20]`: Give gold.
* `[21]`: Give item.
* `[22]`: Give weapon.
* `[26]`: Kick.
* `[27]`: Warn.
* `[28]`: Ban.
* `[34]`: Admin jail.
* `[36]`: Admin stash.
* `[37]`: Open player inventory.
* `[38]`: Clear zone.
* `[39]`: Cuff / uncuff.
* `[40]`: Revive all.
* `[41]`: Heal all.
* `[42]`: Kick all.
* `[43]`: Remove one warning.
* `[44]`: Revive horse.
* `[45]`: Give horse.
* `[46]`: Give wagon.
* `[47]`: Delete identity card.
* `[48]`: Delete fake identity card.
* `[49]`: Create identity card.
* `[50]`: See nearby players.

***

## Ticket System

Ticket settings:

```lua
TicketSystem = true
ReportCommand = "report"
TpBack = true
ModelTicket = "cs_crackpotrobot"
Webhook = "YOUR_TICKET_WEBHOOK"
TicketSolved = "TICKET SOLVED"
TicketTaken = "TICKET TAKEN"
TicketNew = "NEW TICKET"
```

How it works:

1. A player uses the report command.
2. The report form opens.
3. Staff receive the ticket in the admin panel.
4. A staff member can take the ticket.
5. Staff can teleport to the player.
6. When solved, the ticket is marked as solved.
7. If `TpBack = true`, the staff member is teleported back.

To disable the system:

```lua
TicketSystem = false
```

***

## Admin Chat

Admin chat settings:

```lua
AdminChat = true
AdminChatHistoryLimit = 60
```

* `AdminChat`: Enables the admin chat page inside the panel.
* `AdminChatHistoryLimit`: Number of recent messages kept in memory.

The chat history is reset when the resource restarts.

***

## Admin Jail

Admin jail settings:

```lua
AdminJail = {2369.5132, -1492.2881, 45.9974}
JailRadius = 13.0
ReleaseJail = {2680.5466, -1449.5090, 46.3672}
```

* `AdminJail`: Position where jailed players are kept.
* `JailRadius`: Maximum allowed movement distance inside jail.
* `ReleaseJail`: Position where the player is sent after release.

Admin jail time is stored in the database and can persist through reconnects.

***

## Noclip

Noclip keys:

```lua
NoclipSpeed = 0xB2F377E8
NoclipStop = 0x760A9C6F
NoclipUp = 0xD9D0E1C0
NoclipDown = 0x8FFC75D6
```

Noclip speeds are configured in:

```lua
NoClip = {
    Speeds = {
        { speed = 0 },
        { speed = 0.5 },
        { speed = 2 },
        { speed = 5 },
        { speed = 10 },
        { speed = 15 },
    },
}
```

If you are not sure what a key hash does, leave it unchanged.

***

## Webhooks

SS-Admin uses two main webhook fields:

```lua
Webhook = "YOUR_TICKET_WEBHOOK"
WebHook = "YOUR_ADMIN_LOGS_WEBHOOK"
```

* `Webhook`: Ticket system logs.
* `WebHook`: General admin action logs.

Use separate Discord channels if you want ticket logs and admin action logs separated.

***

## Useful Commands

The exact command names are controlled by `Config.Permissions`.

Common default commands include:

* `/adminmenu`
* `/noclip`
* `/tp`
* `/reviveme`
* `/healme`
* `/fix`
* `/delveh`
* `/delhorse`
* `/activeblips`
* `/god`
* `/unban`
* `/spectate`
* `/freeze`
* `/kill`
* `/revive`
* `/heal`
* `/givemoney`
* `/givegold`
* `/giveitem`
* `/giveweapon`
* `/check`
* `/sjob`
* `/notify`
* `/kick`
* `/warn`
* `/ban`
* `/bring`
* `/goto`
* `/ajail`
* `/clearzone`
* `/cuff`
* `/reviveall`
* `/healall`
* `/kickall`
* `/unwarn`
* `/seeplayers`

***

## Exports

SS-Admin exposes report/ticket helper exports:

```lua
exports["SS-Admin"]:ReportList()
exports["SS-Admin"]:Report()
```

Use these only if another resource needs to open the report list or report form directly.

***

## Troubleshooting

### Admin Panel Does Not Open

Check:

* `SS-Core` is started before `SS-Admin`.
* The player has the correct Discord role or Steam identifier.
* Permission `[1]` includes the player's staff category.
* `OpenMenu` is not `false`, or `/adminmenu` is enabled.

### Discord Permissions Do Not Work

Check:

* `UseSteamPermissions = false`.
* Discord bot token is valid.
* The bot is inside the correct Discord server.
* `GuildId` is correct.
* Role IDs are copied correctly.
* The player has Discord linked to RedM identifiers.

### Steam Permissions Do Not Work

Check:

* `UseSteamPermissions = true`.
* The Steam identifier starts with `steam:`.
* The identifier is inside the correct role group.

### Player Cannot Join Because Of Whitelist

Check:

* `WhiteList = true`.
* `WhiteListRoles` contains the correct Discord role IDs.
* The player has one of those roles.
* The Discord bot can read guild member roles.

### Ticket System Does Not Log

Check:

* `TicketSystem = true`.
* `Webhook` contains a valid Discord webhook.
* The player is using the configured `ReportCommand`.

### Admin Voice Does Not Work

Check:

* `AdminVoice = true`.
* `pma-voice` is installed and started.
* Staff has permission to open the admin panel.

### Script Does Not Start

Check:

* Resource folder name is exactly `SS-Admin`.
* `oxmysql` is installed and started before `SS-Admin`.
* `SS-Core` is started before `SS-Admin`.
* SQL has been imported.
* `s/config.lua` exists and does not contain broken Lua syntax.

***

## Recommended Live Checklist

Before going live, confirm:

* SQL has been imported.
* `oxmysql` starts before `SS-Admin`.
* `SS-Core` starts before `SS-Admin`.
* Discord bot token and guild ID are configured if using Discord permissions.
* `UseSteamPermissions` is set correctly.
* Staff roles or Steam identifiers are configured.
* Whitelist is enabled or disabled intentionally.
* Ticket webhook is tested.
* Admin logs webhook is tested.
* `AdminVoice` is disabled if `pma-voice` is not installed.
* One admin account can open the panel.
* Ban, warn, revive, teleport, and ticket actions have been tested.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature.
* `false` disables a feature.
* Numbers do not use quotes: `100`.
* Role IDs, Steam IDs, item names, and webhooks use quotes.
* Do not rename permission indexes.
* Do not paste Discord bot tokens into public messages.

Bad:

```lua
UseSteamPermissions = "false"
```

Good:

```lua
UseSteamPermissions = false
```

Bad:

```lua
[28] = { Command = "ban", Roles = {"ADMIN"} }
[29] = { Command = "bring", Roles = {"ADMIN"} }
```

Good:

```lua
[28] = { Command = "ban", Roles = {"ADMIN"} },
[29] = { Command = "bring", Roles = {"ADMIN"} },
```
