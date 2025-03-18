---
hidden: true
---

# SS-LuckyTicket



<figure><img src="../.gitbook/assets/SS-LuckyTicket.png" alt=""><figcaption><p>SS-LuckyTicket</p></figcaption></figure>

The _SS-LuckyTicket_ script allows you to create customizable scratch tickets with various prize types and chances, adding a fun and interactive lottery-style feature to your server. Here’s a detailed guide to setting it up and maximizing its features.

#### Integrating with SS-Bank

*   **SSBank**: Set to `true` if you have the _SS-Bank_ script and want winning tickets to be redeemable as items at any bank location.

    * When `SSBank = true`, players will receive winning tickets as items in their inventory, which they can take to a bank to redeem.
    * When set to `false`, players receive their winnings instantly.

    {% code overflow="wrap" %}
    ```lua
    SSBank = true  -- Options: true (redeem at bank) / false (instant payout)
    ```
    {% endcode %}

#### 2. Configuring Tickets and Prizes

Each type of ticket (Bronze, Silver, and Gold) has customizable prize options with different winning chances. Adjust the prize amounts and probabilities based on your desired reward structure.

* **Tickets Table**: Each ticket type (`luckyticket`, `luckyticket2`, `luckyticket3`) represents a different tier: Bronze, Silver, and Gold.
  * Each prize option is represented by a prize value (money amount or item name) and a chance percentage.
  * The higher the ticket tier, the greater the potential rewards.

Here’s a breakdown:

**Bronze Ticket (`luckyticket`)**

| Prize     | Chance % | Description             |
| --------- | -------- | ----------------------- |
| `1`       | 15%      | Money amount (1 unit)   |
| `5`       | 10%      | Money amount (5 units)  |
| `25`      | 5%       | Money amount (25 units) |
| `goldbar` | 3%       | Item (Gold Bar)         |

**Silver Ticket (`luckyticket2`)**

| Prize       | Chance % | Description             |
| ----------- | -------- | ----------------------- |
| `5`         | 15%      | Money amount (5 units)  |
| `25`        | 10%      | Money amount (25 units) |
| `50`        | 5%       | Money amount (50 units) |
| `silverbar` | 3%       | Item (Silver Bar)       |

**Gold Ticket (`luckyticket3`)**

| Prize     | Chance % | Description              |
| --------- | -------- | ------------------------ |
| `25`      | 15%      | Money amount (25 units)  |
| `50`      | 10%      | Money amount (50 units)  |
| `100`     | 5%       | Money amount (100 units) |
| `goldbar` | 3%       | Item (Gold Bar)          |

Customize the prizes and chances in each tier based on your server’s economy and desired payout frequency.

#### 3. Customizing In-Game Notifications

The script uses various in-game notifications to communicate the results to players. Here’s a guide to the notification texts you can adjust:

* **"youwin"**: Message displayed upon winning, showing the prize amount.
* **"winnotifybank"**: Message shown when a player wins a ticket item (for _SS-Bank_ redemption).
* **"winnotify"**: Notification displayed for instant cash wins.
* **"youlose"**: Message shown when a player does not win.
* **"notnearbank"**: Notification instructing players to visit a bank for ticket redemption.
* **"winonticket"** & **"loseonticket"**: Text shown directly on the scratch ticket (win/lose message).
* **"scratchInfo"**: Instructions for scratching the ticket.

Example of the configuration for `Translate` table:

```lua
Translate = {
    ["youwin"] = "WIN PRIZE: ",
    ["winnotifybank"] = "You win, redeem the prize at any Bank, Prize: ",
    ["winnotify"] = "CONGRATS! From this ticket, you win ",
    ["youlose"] = "TRY AGAIN, MAYBE MORE LUCK NEXT TIME...",
    ["notnearbank"] = "REDEEM this ticket at any Bank!",
    ["winonticket"] = "💲 ! CONGRATS !💲",
    ["loseonticket"] = "❌ ! YOU LOSE ! ❌",
    ["scratchInfo"] = "Scratch with the cursor, remember to scratch it to the end!",
}
```

#### 4. Custom Notification Function

To further personalize the experience, you can set custom notifications using the `NOTIFY(text)` function. This lets you modify how notifications appear to players.

Default example:

```lua
function NOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000) -- Sends a bottom screen notification for 5 seconds
end
```

Replace `"vorp:TipBottom"` with your server’s notification function if needed.

***

By following this guide, you’ll be able to configure _SS-LuckyTicket_ to match your server’s economy, customize win/loss notifications, and adjust ticket redemption options to suit your preferences.
