# Configuration File

## Main Files

SS-Admin is configured mainly from these files:

* `config.lua`: Main client/server configuration, permissions, commands, ticket settings, admin jail, UI icons, vehicle lists, horse lists, weapon lists, and helper functions.
* `s/config.lua`: Discord bot token and Discord guild ID.
* `l/l.lua`: Lua translations.
* `config.js`: NUI / interface translations.
* `EXTRA/ss_admin.sql`: Database table.

***

## config.lua

{% code overflow="wrap" %}
```lua
Config = {
    Language = "EN",
    AdminVoice = true,
    RoleplayNameList = false,
    OpenMenu = 0x3C3DD371,
    ActiveCommands = true,

    MaxWarns = 3,
    BanWarns = 3,
    MaxWarnsBanReason = "Reached max warns",

    Notify = true,
    PrintUnauthorizedAccess = true,

    NoclipSpeed = 0xB2F377E8,
    NoclipStop = 0x760A9C6F,
    NoclipUp = 0xD9D0E1C0,
    NoclipDown = 0x8FFC75D6,
    NoclipPlayersDistance = 20,

    SpectateStop = 0x760A9C6F,

    ModelTicket = "cs_crackpotrobot",
    TicketSystem = true,
    TpBack = true,
    ReportCommand = "report",
    Webhook = "YOUR_TICKET_WEBHOOK",
    TicketSolved = "TICKET SOLVED",
    TicketTaken = "TICKET TAKEN",
    TicketNew = "NEW TICKET",

    AdminJail = {2369.5132, -1492.2881, 45.9974},
    JailRadius = 13.0,
    ReleaseJail = {2680.5466, -1449.5090, 46.3672},

    BlipsUseSteamName = true,
    BlipsRefresh = 2000,

    AdminChat = true,
    AdminChatHistoryLimit = 60,

    TpEffects = true,
    VolumeEffects = 0.1,
    TimeToCheckBans = 6000 * 60 * 60,
    WebHook = "YOUR_ADMIN_LOGS_WEBHOOK",

    UseSteamPermissions = false,
}
```
{% endcode %}

***

## Discord Bot Config

Open:

```text
s/config.lua
```

{% code overflow="wrap" %}
```lua
Discord = {
    Token = "YOUR_BOT_TOKEN",
    GuildId = "YOUR_DISCORD_SERVER_ID",
}
```
{% endcode %}

Keep the Discord bot token private. If the token is leaked, regenerate it in the Discord developer portal before starting the server again.

***

## Permission Mode

SS-Admin supports two permission modes.

### Discord Role Permissions

{% code overflow="wrap" %}
```lua
UseSteamPermissions = false

DiscordPermissions = {
    {name = "ADMIN", roles = {"ROLE_ID_HERE"}},
    {name = "MODERATOR", roles = {"ROLE_ID_HERE"}},
    {name = "HELPER", roles = {"ROLE_ID_HERE"}},
}
```
{% endcode %}

When this mode is used, the Discord bot checks the player's Discord roles inside the configured guild.

### Steam Identifier Permissions

{% code overflow="wrap" %}
```lua
UseSteamPermissions = true

SteamPermissions = {
    {name = "ADMIN", roles = {"steam:xxxxxxxxxxxx"}},
    {name = "MODERATOR", roles = {}},
    {name = "HELPER", roles = {}},
}
```
{% endcode %}

Use this mode if you do not want to depend on Discord roles for staff permissions.

***

## Whitelist

{% code overflow="wrap" %}
```lua
WhiteList = true
WhiteListRoles = {"DISCORD_ROLE_ID"}
```
{% endcode %}

If `WhiteList = true`, players must have one of the configured Discord roles to join the server.

Set it to `false` if you do not want SS-Admin to handle whitelist access.

***

## Admin Permissions

Every action is controlled by a numeric permission index.

{% code overflow="wrap" %}
```lua
Permissions = {
    [1] = { Command = "adminmenu", Roles = {"ADMIN", "MODERATOR", "HELPER"} },
    [4] = { Command = "noclip", Roles = {"ADMIN", "MODERATOR", "HELPER"} },
    [17] = { Command = "revive", Roles = {"ADMIN", "MODERATOR"} },
    [28] = { Command = "ban", Roles = {"ADMIN"} },
}
```
{% endcode %}

Do not change the numeric indexes. Change only `Command` and `Roles`.

Important indexes:

* `[1]`: Open admin panel.
* `[13]`: Unban.
* `[14]`: Spectate.
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
* `[50]`: See nearby players.

***

## Ticket System

{% code overflow="wrap" %}
```lua
TicketSystem = true
ReportCommand = "report"
TpBack = true
ModelTicket = "cs_crackpotrobot"
Webhook = "YOUR_TICKET_WEBHOOK"
```
{% endcode %}

* `TicketSystem`: Enables player reports and ticket handling.
* `ReportCommand`: Command used by players to open the report form.
* `TpBack`: Sends staff back after solving a ticket.
* `ModelTicket`: Temporary model used during the ticket flow, or `false`.
* `Webhook`: Discord webhook used for ticket logs.

***

## Admin Chat

{% code overflow="wrap" %}
```lua
AdminChat = true
AdminChatHistoryLimit = 60
```
{% endcode %}

Admin chat is shown inside the admin panel for staff members with permission to open the panel. History is stored in memory while the resource is running.

***

## SQL

Import:

```text
EXTRA/ss_admin.sql
```

Main table:

```text
ss_admin
```

Stored data includes identifiers, Discord ID, license, warning count, ban state, playtime, last join/leave timestamps, ban details, and admin jail time.
