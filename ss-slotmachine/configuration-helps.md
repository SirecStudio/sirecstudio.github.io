# Configuration Helps

## SS-SlotMachine Setup & Configuration Guide

SS-SlotMachine is a premium casino slot machine for RedM with a fully server-side payout engine. This guide is written for server owners who want to install, configure, and test the script safely — no Lua knowledge needed.

***

## Dependencies

### Required

* `ghmattimysql`
* `SS-Core`
* `SS-Notify` (or plug your own notify system into `NOTIFY()` at the bottom of `config.lua`)

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```
resources/[scripts]/SS-SlotMachine
```

Keep the resource folder name exactly:

```
SS-SlotMachine
```

### 2. Database — Nothing To Import

On first start the script automatically creates the `ss_slotmachine` table and one row per machine. Each new machine starts with a small seeded bank so it is playable immediately.

### 3. Start Order

```cfg
ensure ghmattimysql
ensure SS-Core
ensure SS-SlotMachine
```

### 4. Set Your Webhook (Optional)

Put your Discord webhook in `s/config.lua` → `ConfigServer.WebHook`. You will receive enter / exit / big-win logs. This file is server-only — the webhook is never downloaded by clients.

### 5. Pick Your Language

`config.lua` → `Config.Language = "EN"` (`EN` / `RO` / `IT` / `DE` / `FR` / `ES` / `PT`). This sets both the in-game texts and the UI automatically.

***

## Adapting The Machine To YOUR Economy

This is **the only thing you must do**. Open `config.lua` and set the bet list to match your server:

```lua
-- small economy server:
Bets = {1, 2, 4, 8, 10, 15, 20, 25},

-- big economy server:
Bets = {10, 25, 50, 100, 200, 300, 400, 500},
```

**That's it.** The highest bet in the list defines the whole machine: every payout phase threshold is computed as a multiple of it, so the machine feels exactly the same on every server — same win frequency, same bonus frequency, same return — only the dollar scale changes.

***

## How The Payout Engine Works

Every machine has its own persistent **bank**:

1. On every spin, the house instantly keeps `HouseEdge` (default 8%) of the bet. The remaining 92% goes into the machine bank.
2. The machine pays wins **only from its bank** — it can never pay money it has not eaten first (wins are hard-capped at the bank).
3. Depending on how full the bank is, the machine moves through phases (thresholds are multiples of your **max bet**):

| Bank level                            | Phase     | Behavior                                                     |
| ------------------------------------- | --------- | ------------------------------------------------------------ |
| below `Small` × MaxBet (default 10×)  | freeze    | pays little, fills its bank                                  |
| above `Small` × MaxBet                | small     | the main phase — feels like a real slot                      |
| above `Normal` × MaxBet (default 25×) | normal    | pays generously, gives money back                            |
| above `Wild` × MaxBet (default 50×)   | **BONUS** | frequent jollies until the bank drops to `WildExit` × MaxBet |

With the default `Bets = {1..25}` this means: bonus mode triggers when a machine has eaten its way up to $1,250 — and then it rains until it is back to $500.

**Player experience with default settings** (verified with multi-million spin simulations):

* \~28% of spins pay something — the machine always feels alive.
* \~32% of 100-spin sessions end in profit — players come back.
* The median player loses only the 8% house edge over a session.
* Global RTP = exactly **92% on every economy** — the house profit is `HouseEdge` × total money wagered, guaranteed.

***

## Tuning The House Profit

Change one value in `s/config.lua`:

```lua
HouseEdge = 0.08, -- 8% house profit (players get 92% back)  <- default, recommended
HouseEdge = 0.15, -- 15% house profit (players get 85% back) <- greedier
HouseEdge = 0.05, -- 5% house profit (players get 95% back)  <- very generous
```

Everything else self-balances automatically.

> ⚠️ The symbol `Weights` in `s/config.lua` are calibrated by simulation. Do **not** change them (or the `Payouts` multipliers in `config.lua`) unless you know how to re-verify the RTP — wrong values can make the machine drain or hoard money.

***

## Adding / Moving Machines

`config.lua` → `Config.Locations`:

```lua
[17] = {x, y, z, heading, "oldslotmachine", true, true},
--                          prop             |     |
--                          show map blip ---+     |
--                          spawn table under -----+
```

Keep the numeric indexes unique and sequential. Each machine gets its own bank row in the database automatically on the next restart.

***

## Discord Webhook Logs

* **Enter / exit**: who sat down at which machine, with their balance.
* **Big wins**: every win of at least `BigWinLog` × bet (default 20×) is posted — so you always know when and where someone hit it big.

***

## Security Notes

* The spin outcome, the win amount and the payment happen **only on the server**. The NUI / client receives the finished result and just animates it.
* The server verifies on every spin: the player **occupies** that machine, is **physically next to it**, the bet is **in your configured list**, and the player **has the money**.
* One machine per player — machines cannot be mass-locked by a cheater.
* Wins are capped at the machine bank — even a hypothetical exploit could never extract more than the machine has swallowed.
* The webhook and the whole payout engine live in `s/config.lua`, which is **never sent to clients**.

***

## Troubleshooting

### The Machine Does Not Spawn / No Prompt

* Ensure `SS-Core` starts before `SS-SlotMachine`.
* Check that the coordinates in `Config.Locations` are valid.

### "This Machine Is Taken" But Nobody Is There

* The previous player crashed mid-session; the slot frees automatically on disconnect. If it persists, `restart SS-SlotMachine`.

### Spin Does Nothing

* Check the server console for MySQL errors — `ghmattimysql` must be started before this script.

### I Changed Bets And The Machine Feels Different

* That is intended: all thresholds re-scale from the new max bet. The _feel_ (win frequency, RTP) stays identical; only the dollar amounts move.

***

## Recommended Live Checklist

Before going live, confirm:

* `ghmattimysql` and `SS-Core` start before `SS-SlotMachine`.
* The startup console shows the table was created / verified.
* `Bets` matches your server economy.
* The webhook in `s/config.lua` is set and tested (optional).
* `Language` is set.
* One full session tested: sit, spin, win, exit — and a disconnect at the machine.

***

## Safe Editing Rules

* Edit **values**, not logic.
* Keep the webhook and payout engine settings in `s/config.lua` only.
* Do not rename the resource folder (it must stay `SS-SlotMachine`).
* If you change `Payouts` or `Weights`, re-verify the RTP before going live.
