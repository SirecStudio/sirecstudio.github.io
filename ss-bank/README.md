---
description: SS-Bank System Script Documentation
---

# SS-Bank

<figure><img src="../.gitbook/assets/RESIZE.png" alt=""><figcaption></figcaption></figure>

**Overview**

**SS-Bank** is the most comprehensive and immersive banking system designed for RedM, featuring an advanced suite of tools for player and director-level financial management. Built for both roleplay immersion and economic depth, SS-Bank offers full support for real-time player banking, gold market simulation, director control systems, salary automation, and secure stash interactions.

This modular system handles all aspects of in-game banking, from classic deposit/withdraw systems to check creation, salary distribution, loan processing, taxation, market price simulation, and gold trading. Players can manage both their **money and gold accounts**, request and repay loans, generate checks, and even access market data with dynamic pricing. Meanwhile, **bank directors** have access to backend controls to manage stashes, freeze accounts, issue salaries, oversee customers, and view logs with full transparency.

Whether you're looking to simulate a historical bank, introduce a functional economy, or roleplay a professional financial director, SS-Bank provides all the tools needed to build a living, breathing economy inside your RedM server.

### Core Banking System

* Full account system for **money and gold** (with separate balances).
* Support for **multiple bank branches** with NPC interaction and director job assignments.
* Each bank has customizable stash capacity, NPC model, distance, and interaction blip.
* **Blacklist item filter** to prevent depositing illegal or dangerous items.
* Directors can be assigned per bank using `Job` and positional configurations.



### Gold Market System

* Real-time **gold buying and selling** based on market prices.
* Fallback prices used if market API is offline (`DefaultBuyGold`, `DefaultSellGold`).
* Option to **manually alter gold market** prices with a custom divisor.
* Separate deposit and withdraw systems for **gold account**.
* Integrated **gold bar item** conversion and tracking.



### Loan Management

* Players can request loans if they meet job conditions and optional identity verification.
* Fully configurable **loan fee**, **repayment plan**, **maximum amount**, and **intervals**.
* Supports compatibility with `SS-IdentityCard` and `SS-Archives` for deeper integration.
* System automatically calculates **loan payback over time** based on configuration.



### Check System

* Players can generate **bank checks** with full detail: name, amount, memo, and expiration.
* Support for **blank/white checks** if no receiver is filled.
* Checks have a configurable cost and minimum value to prevent spam.
* **Custom check item** defined in config (ex: cocoa).
* Optional **alert system for police** if players attempt to deposit stolen/fake checks.



### Director & Staff Tools

* Configurable **director job** per bank.
* Access to a secure **customer stash** system.
* Full **customer view**: account details, gold, loans, transaction history.
* Ability to **freeze/unfreeze accounts** (if enabled).
* Director salary is auto-generated as a **percentage of total bank revenue** (from tax or config).
* Special **backend UI** for managing all financial and customer data.
* NPC-controlled access points and interaction distance to simulate real banking halls.



### Taxation & Salaries

* Enable server-wide **tax system** with configurable rate and intervals.
* Taxes apply to deposits, withdrawals, and salary income.
* Option to **automatically pay player salaries** on intervals (based on bank budget).
* Salary % is configurable and paid from the bank’s collected budget.
* Fully compatible with role-based economy systems.



### Security Stash System

* Secure access system via `SecurityButton`, with configurable stash size per bank.
* Restricted to bank jobs or director only.
* Optional **waiting animation** for immersive RP interaction.



### Transaction History

* Full **transaction log and history** system for director oversight.
* Option to auto-delete transaction history after X days to avoid database bloat.
* Easy access for directors via backend UI.



### Bank Checks & Customer Access

* Detailed **check printing** with signature, expiration, and memo fields.
* Players can print up to `MaxCheckRequests` checks.
* Blank checks can be gifted, traded, or used for in-character transactions.



### Customization & Extensibility

* Full support for multi-language files (`Language = "EN"`)
* Server era/year customizable (`ServerYear = 1899`)
* Optimized logging with optional webhook integration.
* Ready for integration with external systems: SS-IdentityCard, SS-Archives, SS-PoliceJob.
* Supports dynamic economy, historical roleplay, and custom banking strategies.
