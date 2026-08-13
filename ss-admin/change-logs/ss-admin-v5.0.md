# SS-Admin V5.0

## Update Summary

SS-Admin V5.0 is a major update. Staff roles are now created and managed **live from the panel** (stored in the database, instant effect, no restart), a new **Power Admin** ACE system guarantees the owner can never be locked out, all secrets moved server-side, the entire UI was redesigned with **dark / light themes** and responsive scaling up to 4K, database tables now create themselves at startup, and the resource was hardened and optimized for large servers (100–150 players).

***

## Roles & Access — managed from the panel (NEW)

* New **Roles & Access** page in the panel (visible to the Power Admin): create roles, name them, and tick the accesses each role grants.
* A role can be linked to a **Discord role** — everyone holding that role gets the accesses automatically on join — or left on "None — assign manually" and granted per player.
* New **Give Admin** button on the player profile: assign or remove a manual role with one click (matched by steam identifier, works as a toggle).
* New **See Admins** view: lists every admin — manual admins with a **Remove** button, Discord admins shown as "via Discord".
* Online admins now show a 👑 crown next to their name in the Players list.
* Changes apply **instantly** — no config editing, no restart.
* `SteamPermissions` / `DiscordPermissions` were **removed from `config.lua`**: they exposed steam ids and Discord role ids to every client and required a restart to change.
* `Config.Permissions[index]` now only holds `Command` and `Label`; **who** can use each access is decided per role from the panel.

***

## Power Admin (ACE)

* The **Power Admin** is tied to your server ACE setup: whoever holds the `ssadmin.power` ACE (configurable via `Config.PowerAdminAce`) can always open the panel, use every action, and manage roles.
* The script grants the ACE automatically at startup to `group.admin`, `group.superadmin` and `group.mod`. If your admins use a different group, one `add_ace` line in `server.cfg` is enough.

***

## Security Hardening

* Discord bot token, ticket / admin-log webhooks and whitelist role IDs moved to **`s/config.lua`** (server-only — never downloaded by clients).
* Every admin action is now authorized **server-side** from the caller's resolved permission set.
* Added permission checks to server events that previously had none; the world / instance event is now gated behind permission `[35]`.
* Fixed HTML injection (XSS) in the panel through player names, ban fields, tickets and role data.

***

## UI Redesign — Western Premium, Dark & Light

* Panel CSS rewritten from scratch with design tokens and a **dark / light theme** toggle (sun / moon button in the sidebar, remembered per admin).
* **Responsive scaling**: the panel keeps its proportions and stays crisp on 1080p, 2K and 4K.
* Custom Western fonts, new hero-style player info box, and a **WhatsApp-style admin chat** (your messages on the right, others on the left).
* Fixed blurry text and overlapping labels in the report form.

***

## Database — Zero Setup

* `ss_admin` and `ss_admin_roles` tables are **created automatically** at startup, and any missing column is added on older installs (self-healing migration).
* No manual SQL import is needed anymore; `EXTRA/ss_admin.sql` remains as a reference schema only.

***

## Whitelist Safety

* The whitelist is now **fail-open**: if Discord is unreachable (rate limit or outage during a mass restart), players are allowed in instead of being wrongly kicked.

***

## Performance (100–150 Player Servers)

* Discord role lookups are **cached per player** and only happen at connect — role editing, Give Admin and See Admins make zero Discord calls.
* Discord requests have a **bounded timeout**, so a stalled Discord API can never hang the server.
* Client threads (blips, noclip, spectate, see-players, ticket name tags) sleep when inactive — no per-frame cost for non-admins.

***

## Console & Diagnostics

* All diagnostic prints are now gated behind `Config.Debug` (default `false`) for a clean production console.
* New console-only commands: `ssadmin_debug <serverId>` (dumps ACE / identifiers / permissions for a player) and `ssadmin_refresh` (resyncs all online admins).
