# SS-SlotMachine V2.0

## Update Summary

SS-SlotMachine V2.0 is a complete rewrite of the game engine. The whole spin — outcome, win evaluation and payment — now runs **100% server-side**, the payout system was rebuilt as a **real casino RTP engine** with a mathematically guaranteed house edge, and every threshold now **scales automatically to your server economy**. The update also brings full multi-language support, automatic database setup, and Discord big-win logs.

***

## Server-Side Game Engine (Security)

* The server now generates every spin, evaluates every win and pays out — the UI only plays the animation.
* Removed all client events that could be exploited to receive money or reset machine banks.
* On every spin the server validates: the player **occupies** the machine, is **physically next to it**, the bet is **in the configured list**, and the player **has the money**.
* One machine per player — machines cannot be mass-locked.
* The Discord webhook moved to **`s/config.lua`** (server-only — never downloaded by clients).

***

## Real Casino RTP Engine (NEW)

* The house keeps a configurable edge (`HouseEdge`, default **8%**) from every bet; the remaining **92% always returns to the players**. Global RTP = `1 − HouseEdge`, mathematically guaranteed.
* Each machine has a **persistent bank** (stored in the database, survives restarts): it pays only from what it has eaten, and wins are **hard-capped at the bank**.
* The machine moves through phases as its bank fills — freeze → small → normal → **BONUS (wild) mode**, which empties the bank in a rain of jollies.
* Symbol weights per phase were **calibrated with multi-million spin simulations**: \~28% of spins pay something, \~32% of sessions end in profit, and the machine always feels alive.

***

## Scales To Any Economy (NEW)

* Every payout threshold is now a **multiple of your highest bet** instead of a fixed dollar amount.
* Small economy (`Bets = {1..25}`) or big economy (`Bets = {10..500}`) — the machine behaves identically: same win frequency, same bonus frequency, same return. Only the dollar scale changes.
* Adapting the script to your server is now **one config line** (the bet list).

***

## Living Machines

* New machines start with a **seeded bank** so they are playable immediately on a fresh install.
* Machine banks build up over time and periodically trigger the **BONUS mode** — configurable frequency and length via `Steps` in `s/config.lua`.

***

## Discord Webhook Logs

* Player **enter / exit** logs with balance.
* **Big win alerts**: every win of at least `BigWinLog` × bet (default 20×) is posted.

***

## Multi-Language Support (NEW)

* Full translations in Lua (`l/l.lua`) and UI (`config.js`) for `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, `PT`.
* One setting (`Config.Language`) drives both.

***

## Database — Zero Setup (NEW)

* The `ss_slotmachine` table and one row per machine are **created automatically at startup** — no manual SQL import needed.

***

## Fixes

* Fixed machines getting stuck in a low-paying state due to the old fixed-dollar bank thresholds.
* Fixed bet desync between the interface and the game logic.
* Fixed crashes on disconnect while sitting at a machine.
* Fixed machine banks being able to go negative.
* Machines now free themselves safely when a player disconnects mid-session.
