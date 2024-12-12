# Configuration Helps

**Configuration Options**

Below are the customizable options available in the `config.lua` file:

**1. General Settings:**

* **Webhook**: Logging URL for tracking transactions.
* **Dev Mode**: Use `true` for testing and `false` for production.
* **Language**: Default is `EN`. (Add more languages via the `l/l.lua` file.)
* **Server Year**: Default year is `1885` for historical immersion.

***

**2. Interaction Buttons:**

* **Open Bank Menu**: `BankButton = 0x760A9C6F`
* **Security Stash Menu**: `SecurityButton = 0x9959A6F0`
* **Gold Exchange Menu**: `ExchangeButton = 0xD9D0E1C0`
* **Check Menu**: `CheckButton = 0x4BC9DABB`

***

**3. Account Management:**

* Enable account freezing for directors: `CanLock = true`.
* **Gold Bar Item**: Set to `goldbar` for exchanges.

***

**4. Bank Check System:**

* **Enable Checks**: `UseCheck = true` – Activates the check system.
* **Price Per Check**: `PricePerCheck = 10` – Sets the cost for issuing a check. Use `false` to make it free.
* **Check Item**: `CheckItem = "water"` – Defines the in-game item used as a check.
* **Maximum Requests**: `MaxCheckRequests = 10` – Limits the number of checks a player can request at one time.
* **Verify Account Funds**: `CheckMoney = true` – Requires sufficient funds in the account before issuing a check.
* **Fraud Alert**: Notifies police when a player attempts to deposit a check not issued to them: `AlertPolice = true`.

***

**5. Transaction History Settings:**

* Enable transaction logging: `UseHistory = true`.
* Automatic cleanup: Deletes logs older than `30` days: `DeleteAfterDays = 30`.

***

**6. Tax System:**

* Enable taxes: `UseTax = true`.
* Tax collection interval: Every `7` days.
* Tax on withdrawals and deposits: Set to `1%` (adjustable).

***

**7. Loan System:**

* Jobs eligible for loans: Configurable in `Loans.Jobs`.
* Loan fee: `25%` – Example: A $1,000 loan requires $1,250 payback.
* Repayment interval: Every `3` days.
* Maximum loan amount: `$5,000`.
* Additional Requirements:
  * Player must have no pending dossiers: `SSArchives = true`.
  * Identity card required: `SSIdentityCard = true`.

***

**8. Salary System:**

* Payout interval: `60 minutes`.
* Director salary: `0.5%` of the bank budget (e.g., $20,000 in taxes yields $100 salary).

***

**9. Item Restrictions:**

* Blacklist specific items from being banked:
  * Examples: `cigarette`, `weed_leaves`, `lockpick`, `dynamite`.
  * Modify the blacklist under `BlacklistItems`.

***

**10. Bank Configurations:**

Each bank branch can be configured individually:

* **Example Bank Setup**: _Banca Rhodes Union_:
  * ID: `1`.
  * Location: `{1292.82, -1304.67, 76.14, -31.90}`.
  * Director Position: `{1288.12, -1309.54, 77.16}`.
  * Job Required: `PrimarRhodes`.
  * Stash Limit: `300`.
  * Map Marker: `Blip = -2128054417`.
  * Distance for Interaction: `2.5`.

Other banks (Saint Denis, Valentine, Blackwater) follow a similar structure, with unique IDs, positions, and job requirements.
