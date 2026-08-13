---
description: SS-Admin documentation
---

# SS-Admin

<figure><img src="https://2456427394-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FftrmvRh1eQ0kN4kMNPUz%2Fuploads%2FAuQrIuPT72Z6bwQAqBgt%2Fadmin2.png?alt=media&#x26;token=34f4a0f8-cd7c-46da-b3f1-124762389200" alt=""><figcaption></figcaption></figure>

## Overview

**SS-Admin** is an advanced RedM administration panel for server staff. It provides a full NUI admin interface with dark / light themes, a **live Roles & Access system managed entirely from the panel** (no config editing, no restart), player moderation tools, ticket handling, admin chat, admin jail, ban and warn management, and Discord integration for automatic role-based access and whitelist.

The script is designed for live roleplay servers where staff need fast access to player actions, server tools, logs, tickets, and safety controls from one panel — and where the owner needs to manage staff access safely, without exposing ids in config files.

## Main Features

* **Admin Panel Interface**
  * Premium Western-style NUI panel with dashboard, player list, tickets, ban list, give item / weapon tools, wagon and horse tools, and admin chat.
  * **Dark & light theme**, switchable from the sidebar and remembered per admin.
  * **Responsive UI** that scales cleanly on 1080p, 2K and 4K.
  * Optional keybind opening and command-based opening.
* **Roles & Access — managed live from the panel**
  * Create roles and pick the accesses each role grants, directly in the panel — stored in the database, **instant effect, no restart**.
  * Link a role to a **Discord role** (automatic access on join) or assign it **manually per player**.
  * **Give Admin / See Admins** directly from a player's profile; online admins show a 👑 crown in the player list.
  * **Power Admin** via server ACE (`ssadmin.power`) — the owner can never be locked out.
* **Player Moderation Tools**
  * Revive, heal, freeze, kill, spectate, kick, warn, ban, unban, bring, goto, notify, cuff, set job, and admin jail actions.
  * Temporary bans, permanent bans, warning limits, and automatic ban after max warnings.
  * Player death check support with detailed translated damage reasons.
* **Server & Utility Tools**
  * Noclip, god mode, waypoint teleport, coordinate teleport, player blips, nearby player visibility, clear zone, wagon repair / delete, horse delete, and admin stash.
  * Give money, gold, items, weapons, horses, and wagons.
* **Ticket & Staff Communication**
  * Player report command with ticket list for staff.
  * Ticket status flow for new, taken, and solved tickets.
  * **WhatsApp-style admin chat** inside the panel with configurable history size.
* **Security & Reliability**
  * All secrets (Discord bot token, webhooks, whitelist role IDs) live **server-side** in `s/config.lua` — never shipped to clients.
  * Every admin action is authorized server-side from the caller's resolved permissions.
  * Optional Discord whitelist with **fail-open safety**: a Discord outage can never wrongly kick your players.
  * **Database tables are created and verified automatically at startup** — no manual SQL import.
* **Performance**
  * Discord role lookups cached per player (only at connect); bounded API timeouts.
  * Client threads sleep when inactive — no per-frame cost for non-admins. Built for 100–150 player servers.
* **Integrations**
  * Required integration with `SS-Core`; database storage through `oxmysql`.
  * Optional admin voice support through `pma-voice`.
  * Admin actions for `SS-Stable` horse tools and `SS-IdentityCard` identity creation / removal flows.
* **Multi-Language Support**
  * Lua translations and UI translations for multiple languages.
  * Default language support for `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, and `PT`.
