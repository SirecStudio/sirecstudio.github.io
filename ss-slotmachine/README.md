---
description: SS-SlotMachine documentation
---

# SS-SlotMachine

## Overview

**SS-SlotMachine** is a premium RedM casino slot machine with a **fully server-side, real-casino payout engine**. The house edge is mathematically guaranteed, the payout behavior **scales automatically to your server economy**, and the whole game logic runs on the server — nothing a cheater can touch.

Each machine is a living machine with its own **persistent bank**: it pays only from what it has eaten, builds up over time, and periodically enters a **BONUS (wild) mode** that empties its bank in a rain of jollies.

## Main Features

* **Slot Machine Interface**
  * Beautiful western-style NUI — 5 reels, 6 symbols, animated lever, paytable, and sounds.
  * Map blips per machine (optional), busy-machine protection, safe cleanup on disconnect / restart.
* **100% Server-Side Game Engine**
  * The server generates every spin, computes every win and pays out; the UI only plays the animation.
  * There is no client event that can be exploited to receive money.
* **Real Casino RTP System**
  * The house keeps a configurable edge (default **8%**) from every bet; the remaining **92% always returns to the players**.
  * Just like a real casino: many players win their session, the house wins the month — guaranteed.
* **Scales To Any Economy Automatically**
  * Every payout threshold is a multiple of your **highest bet**.
  * Whether your server plays with $1–$25 or $10–$500 bets, the machine behaves identically — same win frequency, same bonus frequency, same return.
* **Living Machines With Persistent Banks**
  * Each machine has its own bank stored in the database (survives restarts).
  * Wins are paid **only from the machine bank** — a machine can never pay money it has not eaten first.
  * When the bank fills up, the machine enters **BONUS mode** with frequent jollies until the bank drains back down.
* **Anti-Cheat Protection**
  * Server validates machine occupancy, physical distance, and the bet whitelist on every spin.
  * One machine per player; wins are hard-capped at the machine bank.
* **Discord Webhook Logs**
  * Player enter / exit logs with balance.
  * **Big win alerts** for every win of at least a configurable multiple of the bet.
* **Zero Database Setup**
  * The `ss_slotmachine` table is **created automatically at startup** — no manual SQL import needed.
* **Integrations**
  * Required integration with `SS-Core`; database storage through `ghmattimysql`.
  * Notifications through `SS-Notify` (or plug in your own notify system with one function).
* **Multi-Language Support**
  * Lua translations and UI translations, driven by one setting.
  * Default language support for `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, and `PT`.
