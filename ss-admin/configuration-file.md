# Configuration File

## Main Files

SS-Admin is configured mainly from these files:

* `config.lua`: Main configuration — **shipped to clients, so it contains no secrets**: general settings, ticket settings, admin jail, noclip keys, the permissions catalog (`Command` + `Label`), `PowerAdminAce`, and the whitelist on / off switch.
* `s/config.lua`: **Server-only secrets** — Discord bot token, guild ID, ticket / admin-log webhooks, and whitelist Discord role IDs. Never sent to clients.
* `l/l.lua`: Lua translations.
* `config.js`: NUI / interface translations.
* `EXTRA/ss_admin.sql`: Reference schema only — **the script creates and verifies the tables automatically at startup**.

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
    Debug = false,

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

    PowerAdminAce = "ssadmin.power",
    WhiteList = true,
}
```
{% endcode %}

* `Debug`: Set `true` only while testing — prints permission / connect / Discord diagnostics to the server console. Keep `false` in production.
* Webhooks are **no longer in `config.lua`** — they moved to `s/config.lua` so clients can never read them.

***

## Server Secrets (`s/config.lua`)

This file is loaded **only on the server** — nothing in it is ever sent to players.

{% code overflow="wrap" %}
```lua
Discord = {
    Token = "YOUR_BOT_TOKEN",
    GuildId = "YOUR_DISCORD_SERVER_ID",
}

Config = Config or {}
Config.WebHook = "YOUR_ADMIN_LOGS_WEBHOOK"   -- general admin action logs
Config.Webhook = "YOUR_TICKET_WEBHOOK"       -- ticket system logs
Config.WhiteListRoles = {"DISCORD_ROLE_ID"}  -- whitelist role IDs
```
{% endcode %}

Keep the Discord bot token private. If the token is leaked, regenerate it in the Discord developer portal before starting the server again.

***

## Roles & Access — Managed From The Panel

Staff roles are **no longer configured in `config.lua`**. The old `DiscordPermissions` / `SteamPermissions` tables were removed — they exposed steam ids and Discord role ids to every client and required a restart to change.

Everything is now managed **live from the panel** and stored in the database (`ss_admin_roles`), so changes apply instantly with no restart:

* Open the panel as **Power Admin** → **Roles & Access** (sidebar).
* **New Role** → name it and tick the accesses it should grant.
* Optionally link it to a **Discord role** (automatic access on join), or leave it manual and use **Give Admin** on a player's profile.
* **See Admins** lists every admin — manual ones are removable, Discord ones are managed from Discord.

***

## Power Admin (ACE)

The Power Admin can always open the panel, use every action, and manage roles. It is tied to your server ACE setup, so it can never be locked out:

{% code overflow="wrap" %}
```cfg
add_principal identifier.steam:110000XXXXXXXXX group.admin
```
{% endcode %}

The script automatically grants the `ssadmin.power` ACE to `group.admin`, `group.superadmin` and `group.mod` at startup. If your admins use a different group, add one line to `server.cfg`:

{% code overflow="wrap" %}
```cfg
add_ace group.yourgroup ssadmin.power allow
```
{% endcode %}

The ACE object checked is set by `Config.PowerAdminAce` (default `ssadmin.power`).

***

## Whitelist

The on / off switch stays in `config.lua`:

{% code overflow="wrap" %}
```lua
WhiteList = true
```
{% endcode %}

The allowed Discord role IDs live **server-side** in `s/config.lua` → `Config.WhiteListRoles` (never sent to clients).

**Fail-open safety:** if Discord is unreachable (e.g. rate-limited during a mass restart), players are **allowed in** instead of being wrongly kicked.

***

## Permissions Catalog

Every action is controlled by a numeric permission index. Each entry now only holds the `Command` and a `Label` (shown in the Roles editor). **Who** can use each access is decided per role from the panel.

{% code overflow="wrap" %}
```lua
Permissions = {
    [1]  = { Command = "adminmenu",  Label = "Open admin panel" },
    [4]  = { Command = "noclip",     Label = "Noclip" },
    [17] = { Command = "revive",     Label = "Revive player" },
    [28] = { Command = "ban",        Label = "Ban" },
}
```
{% endcode %}

* `Command`: Chat command for that action, or `false` for panel-button only.
* `Label`: Name shown for this access in the panel Roles editor.

Do not change the numeric indexes. Change only `Command` and `Label`.

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
* `[35]`: New world / instance.
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
```
{% endcode %}

* `TicketSystem`: Enables player reports and ticket handling.
* `ReportCommand`: Command used by players to open the report form.
* `TpBack`: Sends staff back after solving a ticket.
* `ModelTicket`: Temporary model used during the ticket flow, or `false`.
* The ticket webhook is set in `s/config.lua` (`Config.Webhook`).

***

## Admin Chat

{% code overflow="wrap" %}
```lua
AdminChat = true
AdminChatHistoryLimit = 60
```
{% endcode %}

Admin chat is shown inside the admin panel for staff members with permission to open the panel — WhatsApp style, with your messages on the right and other admins on the left. History is stored in memory while the resource is running.

***

## Database

You do **not** need to import any SQL. On first start SS-Admin automatically:

* creates the `ss_admin` and `ss_admin_roles` tables if they do not exist,
* adds any missing column on older installs (self-healing migration).

The reference schema is still in `EXTRA/ss_admin.sql` if you want to inspect it. Stored data includes identifiers, Discord ID, license, warning count, ban state, playtime, last join / leave timestamps, ban details, admin jail time, and the panel-managed roles.
