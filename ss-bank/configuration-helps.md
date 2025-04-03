---
description: SS-Bank Configuration Guide
---

# Configuration Helps

**SS-Bank Configuration Guide**



Below are the customizable options available in the `config.lua` file:

### **General Settings**

* **`Dev`**: `true`\
  Enables developer/debug mode. Set to `false` on production servers.
* **`Language`**: `EN`\
  Language file used (must match a file inside `l/l.lua`).
* **`WebHook`**: `""`\
  Discord Webhook for logging bank transactions and actions.
* **`WaitingAnime`**: `false`\
  Enables a short idle animation when accessing bank menus (for immersion).
* **`ServerYear`**: `1899`\
  Used for check stamping and timeline simulation.

***

### Permissions and Features

* **`CanLock`**: `false`\
  Allows bank directors to freeze or unfreeze player accounts.
* **`UseCheck`**: `true`\
  Enables the bank check system.
* **`UseHistory`**: `true`\
  Enables transaction history tracking. Requires SQL table `bank_history`.
* **`SSArchives`**: `false`\
  If `true`, players with a criminal record cannot take loans (requires SS-Archives).
* **`SSIdentityCard`**: `false`\
  If `true`, players need a valid identity card to apply for loans (requires SS-IdentityCard).

***

### Bank Interaction Buttons

* **`BankButton`**: `0x760A9C6F`\
  Keybind for opening the standard bank menu.
* **`SecurityButton`**: `0x9959A6F0`\
  Keybind for accessing the secure stash (for directors only).
* **`ExchangeButton`**: `0xD9D0E1C0`\
  Keybind to open the currency/gold exchange interface.
* **`CheckButton`**: `0x4BC9DABB`\
  Keybind to access the check creation menu.

***

### Gold and Check System

* **`GoldBarItem`**: `"goldbar"`\
  Item name used for gold deposits/withdrawals.
* **`MinAmount`**: `5`\
  Minimum amount to write a check. Set to `0` to disable checks below this value.
* **`PricePerCheck`**: `2`\
  Cost in dollars for creating each check. Set to `false` for free checks.
* **`CheckItem`**: `"cocoa"`\
  Item given to players that represents a check.
* **`MaxCheckRequests`**: `10`\
  Maximum number of checks a player can generate.
* **`AlertPolice`**: `false`\
  If enabled, alerts police when someone tries to deposit a stolen check.

***

### Loan Configuration

* **`Fee`**: `25`\
  Percentage added on top of the requested loan. Example: a $1,000 loan with a 25% fee means total to repay = $1,250.
* **`PayBacks`**: `20`\
  Percentage of the original loan repaid on each installment. Example: 20% of $1,000 = $200 per interval.
* **`LoanTime`**: `3`\
  Number of **days** between each loan repayment.
* **`MaxLoan`**: `5000`\
  Maximum loan value a player can request.
* **`Jobs`**: `{ "civilian", "blacksmith", "farmer" }`\
  List of jobs allowed to take loans.

***

### Salary & Tax System

* **`SalaryTime`**: `60`\
  Time interval (in minutes) between salary payouts for the bank director.
* **`DirectorSalary`**: `0.5`\
  Percentage of total bank budget (from taxes) paid as director salary.\
  Example: If `DirectorSalary = 0.5` and bank has $20,000, payout = $100.
* **`UseTax`**: `false`\
  Enables tax system for withdrawals and deposits. Must be `true` to activate `Tax*` values below.
* **`TaxTime`**: `7`\
  Time interval (in days) between automatic tax collection.
* **`TaxPrice`**: `1`\
  Tax percentage for general income (used with `Salary` and budget logic).
* **`TaxWithdraw`**: `1`\
  Percentage taxed when a player withdraws money.
* **`TaxDeposit`**: `1`\
  Percentage taxed when a player deposits money.

***

### Transaction History

* **`UseHistory`**: `true`\
  Enables transaction logging and history (requires SQL table `bank_history`).
* **`DeleteAfterDays`**: `30`\
  Auto-deletes transactions older than the configured number of days (to prevent database overload).

***

### Item Blacklist

**`BlacklistItems`**\
A table of item names that cannot be deposited into the bank stash (for security).\
Example:

```lua
BlacklistItems = {
    "explosive",
    "dynamite",
    "illegal_documents"
}
```



***

### Bank Branches (Multi-Bank System)

Each entry inside `Banks = {}` defines a bank branch:

#### Example:

```lua
luaCopiaModifica[1] = {
    Name = "NewHorizon Bank Rhodes",
    Id = 1,
    Active = true,
    Bank = "Rhodes",
    Stash = 300,
    Pos = {1292.82, -1304.67, 76.14, -31.90},
    Director = {1288.12, -1309.54, 77.16},
    Job = "PrimarRhodes",
    Npc = "s_m_m_bankclerk_01",
    Blip = -2128054417,
    Distance = 2.5,
}
```

#### Description of fields:

* **`Name`**\
  Displayed name of the bank (appears on UI, receipts, and logs).
* **`Id`**\
  Unique identifier for the bank. Also used for integrations (e.g., SS-BankHeist).
* **`Active`**\
  Enables or disables this branch. If `false`, it won’t appear in-game.
* **`Bank`**\
  Internal name used in logs and backend. Do **not** rename unless you know what you're doing.
* **`Stash`**\
  Maximum number of slots in the bank’s secure stash.
* **`Pos`**\
  Coordinates and heading for the player interaction point (bank entrance).
* **`Director`**\
  Coordinates for the director UI menu (back office).
* **`Job`**\
  Required job to access director features for this branch.
* **`Npc`**\
  The ped model for the bank NPC. Set to `false` to disable.
* **`Blip`**\
  Map blip ID. Set to `false` to hide the bank on the map.
* **`Distance`**\
  Distance at which players can interact with the NPC/menu.
