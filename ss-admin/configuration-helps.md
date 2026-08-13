# Configuration Helps

## SS-Admin Setup & Configuration Guide

SS-Admin is an advanced admin panel and staff toolset for RedM. It includes player moderation actions, ticket reports, admin chat, admin jail, a **live Roles & Access system managed from the panel**, optional Discord whitelist, server utility tools, economy tools, and integrations with other Sirec Studio systems.

This guide is written for server owners who want to install, configure, and test the script safely — no Lua knowledge needed.

***

## Features Overview

SS-Admin includes:

* NUI admin panel with dashboard, player tools, tickets, ban list, item / weapon tools, horse tools, wagon tools, and admin chat — **dark & light theme**, responsive on 1080p / 2K / 4K.
* **Roles & Access managed live from the panel** — Discord-linked or manual roles, instant effect, no restart.
* Staff actions such as revive, heal, freeze, kill, spectate, bring, goto, kick, warn, ban, unban, notify, cuff, and admin jail.
* Utility tools such as noclip, god mode, waypoint teleport, coordinate teleport, player blips, nearby player visibility, clear zone, and admin stash.
* Economy tools for giving money, gold, items, and weapons.
* Horse and wagon admin tools.
* Ticket system with player report command.
* WhatsApp-style admin chat with configurable in-memory history.
* Optional Discord whitelist with **fail-open safety**.
* **Automatic database setup** — tables create and verify themselves at startup.
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

If you do not use the related scripts, simply do not grant the matching accesses to your roles.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```
resources/[scripts]/SS-Admin
```

Keep the resource folder name exactly:

```
SS-Admin
```

### 2. Database — Nothing To Import

You do **not** need to import any SQL. On first start SS-Admin automatically creates the `ss_admin` and `ss_admin_roles` tables and adds any missing column on older installs (self-healing migration). The reference schema stays in `EXTRA/ss_admin.sql` if you want to inspect it.

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

### 4. Set Your Power Admin (server.cfg)

The **Power Admin** can always open the panel, use every action, and manage roles. It is tied to your server ACE admin group, so it can never be locked out.

If your admins are already in `group.admin` (the standard setup):

```cfg
add_principal identifier.steam:110000XXXXXXXXX group.admin
```

That's it — the script grants the `ssadmin.power` ACE to `group.admin`, `group.superadmin` and `group.mod` automatically at startup.

If your admins are in a **different** group, add one line:

```cfg
add_ace group.yourgroup ssadmin.power allow
```

The ACE object checked is set by `Config.PowerAdminAce` in `config.lua` (default `ssadmin.power`).

### 5. Restart The Server

Restart fully and test with one staff account before opening the server to players. On start you should see:

```
SS-Admin database: tables verified / created, columns checked
SS-Admin roles: N role(s) loaded from database
```

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main script configuration (shipped to clients — **no secrets here**).
* `s/config.lua`: **Server-only secrets** — Discord bot token, guild ID, webhooks, whitelist role IDs.
* `l/l.lua`: Lua translations.
* `config.js`: UI translations.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Admin panel UI.
* `EXTRA/ss_admin.sql`: Reference schema only.

***

## Languages

The main language is configured in `config.lua`:

```lua
Language = "EN"
```

Included languages: `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, `PT`.

Lua translations are in `l/l.lua`, UI translations in `config.js`.

***

## First Configuration

Open `config.lua` and start with the general settings:

```lua
Language = "EN"
AdminVoice = true
RoleplayNameList = false
OpenMenu = 0x3C3DD371
ActiveCommands = true
MaxWarns = 3
BanWarns = 3
Notify = true
Debug = false
```

* `Language`: Main language used by Lua notifications and supported UI text.
* `AdminVoice`: Sends staff to the admin voice channel when they have admin access.
* `RoleplayNameList`: Uses character names instead of Steam names in player lists and commands.
* `OpenMenu`: Key hash used to open the admin panel, or `false` to disable key opening.
* `ActiveCommands`: Enables admin commands such as `/kick`, `/ban`, `/tp`, `/givemoney`, and `/giveitem`.
* `MaxWarns`: Number of warnings before automatic ban.
* `BanWarns`: Number of days for the automatic ban.
* `Notify`: Sends notifications for admin actions.
* `Debug`: Keep `false` in production. Set `true` only while testing — prints permission / connect / Discord diagnostics.

***

## Discord Bot Setup

Only needed if you use **Discord-linked roles** or the **Discord whitelist**.

Open `s/config.lua` and set:

```lua
Discord = {
    Token = "YOUR_BOT_TOKEN",
    GuildId = "YOUR_DISCORD_SERVER_ID",
}
```

The bot must be **inside your Discord server**. On start the console prints whether the bot connected:

```
SS-Admin Discord bot connected: <Your Server> (<id>)
```

Keep the token private. Never share it publicly or include it in screenshots.

***

## Managing Admin Roles (From The Panel)

Roles are **no longer configured in `config.lua`** — that was a security risk (steam ids / role ids were downloaded by every client). Everything is now managed live from the panel and stored in the database, so **changes apply instantly, no restart**.

Open the panel as Power Admin → **Roles & Access** (sidebar).

### Create A Role

* **New Role** → give it a name and tick the accesses it should have.
* **Discord role (optional):**
  * Pick a Discord role → everyone with that role gets the accesses **automatically on join**.
  * Leave it on **"None — assign manually"** → the role is granted per player with **Give Admin** (below).

### Give / Remove Admin On A Specific Player

* Open a player's profile (Players → click a name) → **Give Admin** button.
* Pick one of your roles → the player gets it (matched by their steam id). Click again to remove (toggle).

### See Who Is Admin

* **See Admins** (next to New Role) lists every admin:
  * **Manual** admins → shown with a **Remove** button.
  * **Discord** admins → shown as "via Discord" (manage them from Discord).
* Online admins also get a 👑 **crown** next to their name in the Players list.

***

## Whitelist

* Toggle with `Config.WhiteList` in `config.lua`.
* The allowed Discord role IDs live **server-side** in `s/config.lua` → `Config.WhiteListRoles` (never sent to clients).
* **Fail-open safety:** if Discord is unreachable (e.g. rate-limited during a mass restart), players are **allowed in** instead of being wrongly kicked.

If your server does not use SS-Admin for whitelist access, set `WhiteList = false`.

***

## Theme (Dark / Light)

Each admin can switch **dark / light** from the sun / moon button in the sidebar. The choice is remembered per admin (stored locally in the panel).

***

## Ticket System

Ticket settings in `config.lua`:

```lua
TicketSystem = true
ReportCommand = "report"
TpBack = true
ModelTicket = "cs_crackpotrobot"
```

The ticket webhook is set in `s/config.lua` (`Config.Webhook`).

How it works:

1. A player uses the report command.
2. The report form opens.
3. Staff receive the ticket in the admin panel.
4. A staff member can take the ticket.
5. Staff can teleport to the player.
6. When solved, the ticket is marked as solved.
7. If `TpBack = true`, the staff member is teleported back.

To disable the system, set `TicketSystem = false`.

***

## Admin Chat

```lua
AdminChat = true
AdminChatHistoryLimit = 60
```

* `AdminChat`: Enables the admin chat page inside the panel — WhatsApp style (your messages right, others left).
* `AdminChatHistoryLimit`: Number of recent messages kept in memory.

The chat history is reset when the resource restarts.

***

## Admin Jail

```lua
AdminJail = {2369.5132, -1492.2881, 45.9974}
JailRadius = 13.0
ReleaseJail = {2680.5466, -1449.5090, 46.3672}
```

* `AdminJail`: Position where jailed players are kept.
* `JailRadius`: Maximum allowed movement distance inside jail.
* `ReleaseJail`: Position where the player is sent after release.

Admin jail time is stored in the database and persists through reconnects.

***

## Noclip

Noclip keys:

```lua
NoclipSpeed = 0xB2F377E8
NoclipStop = 0x760A9C6F
NoclipUp = 0xD9D0E1C0
NoclipDown = 0x8FFC75D6
```

If you are not sure what a key hash does, leave it unchanged.

***

## Webhooks

Both webhooks now live **server-side** in `s/config.lua`:

```lua
Config.WebHook = "YOUR_ADMIN_LOGS_WEBHOOK"  -- general admin action logs
Config.Webhook = "YOUR_TICKET_WEBHOOK"      -- ticket system logs
```

Use separate Discord channels if you want ticket logs and admin action logs separated.

***

## Useful Commands

The exact command names are controlled by `Config.Permissions`. Common default commands include:

* `/adminmenu`, `/noclip`, `/tp`, `/god`, `/spectate`
* `/revive`, `/heal`, `/reviveall`, `/healall`, `/reviveme`, `/healme`
* `/kick`, `/warn`, `/unwarn`, `/ban`, `/unban`, `/ajail`
* `/givemoney`, `/givegold`, `/giveitem`, `/giveweapon`
* `/bring`, `/goto`, `/freeze`, `/kill`, `/cuff`, `/notify`
* `/fix`, `/delveh`, `/delhorse`, `/activeblips`, `/clearzone`, `/seeplayers`, `/check`, `/sjob`

### Server Console Diagnostics

* `ssadmin_debug <serverId>`: Dumps ACE / identifiers / permissions for a player.
* `ssadmin_refresh`: Resyncs permissions for all online admins.

***

## Exports

SS-Admin exposes report / ticket helper exports:

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
* Set `Config.Debug = true` and check the server console for `perms sync: [id] name ... power admin: true/false`.
* If `power admin: false`, your character's steam id is not in `group.admin` — add it (see Installation step 4), then `refresh` + `restart SS-Admin`.
* Otherwise, make sure a role granting access `[1]` (Open admin panel) is assigned to you from the Roles & Access page.
* `ssadmin_debug <id>` and `ssadmin_refresh` (server console only) help diagnose.

### Discord Roles Do Not Resolve

Check:

* Token and `GuildId` in `s/config.lua` are correct.
* The bot is inside the correct Discord server.
* The role picked in the panel Roles editor is the right one.
* The player has Discord linked to their RedM identifiers.

### Player Wrongly Kicked By Whitelist

The whitelist is fail-open on Discord errors, so an outage never kicks players. If a specific player is kicked:

* Confirm they have a whitelisted role.
* Confirm `Config.WhiteListRoles` (in `s/config.lua`) contains the correct role IDs.

### Ticket System Does Not Log

Check:

* `TicketSystem = true`.
* `Config.Webhook` in `s/config.lua` contains a valid Discord webhook.
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
* `s/config.lua` exists and does not contain broken Lua syntax.

***

## Recommended Live Checklist

Before going live, confirm:

* `oxmysql` and `SS-Core` start before `SS-Admin`.
* The startup console shows `tables verified / created` (no SQL import needed).
* Your Power Admin can open the panel (ACE group set in `server.cfg`).
* Roles are created in **Roles & Access** and assigned (Discord or manual).
* Discord bot token and guild ID are configured if using Discord roles or whitelist.
* Whitelist is enabled or disabled intentionally.
* Ticket webhook and admin logs webhook (both in `s/config.lua`) are tested.
* `AdminVoice` is disabled if `pma-voice` is not installed.
* `Config.Debug` is set back to `false`.
* Ban, warn, revive, teleport, and ticket actions have been tested.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature, `false` disables it.
* Numbers do not use quotes: `100`.
* Role IDs, item names, and webhooks use quotes.
* Do not change the numeric permission indexes.
* Keep secrets (token, webhooks, whitelist role IDs) **only** in `s/config.lua`.
* Do not paste Discord bot tokens into public messages.

Bad:

```lua
WhiteList = "false"
```

Good:

```lua
WhiteList = false
```
