# Configuration File

## Main Files

SS-SlotMachine is configured mainly from these files:

* `config.lua`: Main configuration — **shipped to clients, so it contains no secrets**: language, open key, bets, machine locations, paytable, and the notification function.
* `s/config.lua`: **Server-only** — Discord webhook and the whole payout engine (house edge, phase thresholds, seed bank, big-win threshold, symbol weights). Never sent to clients.
* `l/l.lua`: Lua translations.
* `config.js`: NUI / interface translations.
* `s/s.lua`: Server game engine.
* `c/c.lua`: Client (props, blips, prompts, NUI bridge).
* `UI/`: The slot machine interface.

***

## config.lua

{% code overflow="wrap" %}
```lua
Config = {
    Language = "EN",       -- EN / RO / IT / DE / FR / ES / PT
    Key = 0xD9D0E1C0,      -- key to open the slot machine
    Blips = 1243830185,    -- blip sprite used on the map
    Distance = 1.5,        -- how close the player must be to get the prompt

    Bets = {1, 2, 4, 8, 10, 15, 20, 25},

    UseTable = "p_plantstand01x", -- prop used as table under the machine

    Locations = {
        [1] = {-310.0323, 798.0159, 118.0197, -123.3176, "oldslotmachine", false, true},
        -- ... one entry per machine (16 included by default)
    },

    Payouts = {
        jolly     = { [5]=100 },
        badge     = { [2]=4,   [3]=16,  [4]=25, [5]=50 },
        shoes     = { [3]=12,  [4]=20,  [5]=30 },
        wagon     = { [3]=8,   [4]=14,  [5]=20 },
        horse     = { [2]=2,   [3]=4,   [4]=8,  [5]=16 },
        revolver  = { [2]=1,   [3]=2,   [4]=6,  [5]=12 },
    },
}
```
{% endcode %}

***

## Bets — The Only Thing You Must Adapt

The **highest bet in the list defines the whole machine**: every payout phase threshold is computed as a multiple of it, so the machine feels exactly the same on every server — same win frequency, same bonus frequency, same return — only the dollar scale changes.

{% code overflow="wrap" %}
```lua
-- small economy server:
Bets = {1, 2, 4, 8, 10, 15, 20, 25},

-- big economy server:
Bets = {10, 25, 50, 100, 200, 300, 400, 500},
```
{% endcode %}

***

## Machine Locations

{% code overflow="wrap" %}
```lua
[17] = {x, y, z, heading, "oldslotmachine", true, true},
--                          prop             |     |
--                          show map blip ---+     |
--                          spawn table under -----+
```
{% endcode %}

Keep the numeric indexes unique and sequential. Each machine gets its own bank row in the database automatically on the next restart.

***

## Paytable

`Config.Payouts` maps `[how many symbols in a row from the left] = multiplier`. **JOLLY** substitutes any symbol; 5× JOLLY pays 100× the bet.

> ⚠️ If you change these values, also update the paytable in `UI/UI.html` and re-verify the RTP — wrong values can make the machine unprofitable for the house. The shipped values are calibrated by simulation.

***

## Server Config (`s/config.lua`)

This file is loaded **only on the server** — nothing in it is ever sent to players.

{% code overflow="wrap" %}
```lua
ConfigServer = {
    WebHook = "YOUR_DISCORD_WEBHOOK", -- enter / exit / big win logs

    HouseEdge = 0.08, -- 8% house profit; players get 92% back

    Steps = {
        Small    = 10, -- bank >= 10 x MaxBet -> "small" phase
        Normal   = 25, -- bank >= 25 x MaxBet -> "normal" phase
        Wild     = 50, -- bank >= 50 x MaxBet -> BONUS mode
        WildExit = 20, -- bonus ends below 20 x MaxBet
    },

    SeedBank = 12,  -- starting bank for new machines (x MaxBet)
    BigWinLog = 20, -- wins >= 20 x bet are logged on the webhook

    Weights = {
        -- symbol weights per phase, calibrated by simulation
        -- DO NOT change without re-verifying the RTP
    },
}
```
{% endcode %}

* `HouseEdge`: The % of every bet the house keeps. Global RTP is mathematically guaranteed = `1 - HouseEdge`:

{% code overflow="wrap" %}
```lua
HouseEdge = 0.08, -- 8% house profit (players get 92% back)  <- default, recommended
HouseEdge = 0.15, -- 15% house profit (players get 85% back) <- greedier
HouseEdge = 0.05, -- 5% house profit (players get 95% back)  <- very generous
```
{% endcode %}

* `Steps`: Phase thresholds in multiples of your max bet — controls how often the BONUS triggers and how long it lasts.
* `SeedBank`: New machines start with this bank (× max bet) so they are playable immediately on a fresh install.
* `BigWinLog`: Webhook alert threshold, as a multiple of the bet.
* `Weights`: Symbol weights per phase, **calibrated by simulation** — do not change them unless you know how to re-verify the RTP.

***

## Notifications

Plug in your own notify system at the bottom of `config.lua`:

{% code overflow="wrap" %}
```lua
function NOTIFY(text)
    exports["SS-Notify"]:Notify("INFO", "~#ffcc00~Slot Machine!~e~", text, "notify_dead_drop", 6000, "middle-left", "circle", "#ffcc00")
end
```
{% endcode %}

***

## Database

You do **not** need to import any SQL. On first start the script automatically creates the `ss_slotmachine` table and one row per machine. Each new machine starts with a small seeded bank so it is playable immediately.
