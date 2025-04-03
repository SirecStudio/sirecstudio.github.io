# Configuration File

### config.lua

{% code overflow="wrap" %}
```lua
-- Author: SIREC
-- Report any bugs on: https://discord.gg/9XNBaQSmMd

Config = {

    -- Logging and Development Settings
    WebHook = "", -- Webhook URL for logging
    Dev = true, -- Set to `true` for testing; `false` for production
    Language = "EN", -- Language (check `l/l.lua` for available options)
    WaitingAnime = false, -- Enable Random Waiting Animation while using bank ? 8 for female, 8 for male (RP Improve)
    ServerYear = 1899,

    -- Interaction Buttons
    BankButton = 0x760A9C6F, -- Open Bank Button
    SecurityButton = 0x9959A6F0, -- Open Security Stash Button
    ExchangeButton = 0xD9D0E1C0, -- Exchange Button
    CheckButton = 0x4BC9DABB, -- Ask checks buttont/t

    -- Account Management
    CanLock = false, -- Allow Director to freeze player accounts
    GoldBarItem = "goldbar", -- Item used for gold bar exchange
    
    -- Check Settings
	UseCheck = true, -- Enable check system ?
    MinAmount = 5, -- Min amount to sign a check, 0 di disable
    PricePerCheck = 2, -- Price to pay for every check, false to disable and being free
    CheckItem = "cocoa", -- Check item to use 
	MaxCheckRequests = 10, -- Max checks a player can ask
	AlertPolice = false, -- Alert Police when somebody try deposit a check of somebody else ?
    
    -- History Settings
    UseHistory = true, -- Enable Transaction history (You need have the sql for bank_history)
    DeleteAfterDays = 30, -- Auto delete transactions after X days ! (Helps cleaning database)
    
    
    -- Tax Settings
    UseTax = false, -- Enable taxes for players
    TaxTime = 7, -- Interval (days) for tax collection
    TaxPrice = 1, -- Tax percentage (e.g., 1% of $50,000 is $500)
    TaxWithdraw = 1, -- Tax percentage on withdrawals
    TaxDeposit = 1, -- Tax percentage on deposits

    -- Item Restrictions
    BlacklistItems = { -- Restricted items for banking
        "cigarette", "weed_leaves", "heroin", "opium", "morphine", "cigar", "joint",
        "weedbags", "hashish", "lockpick", "ammodynamite", "smallbomb", "bigbomb",
        "ammopoisonbottle", "handcuffs", "handcuffskey", "typhus_injection"
    },

    -- Loan Settings
    Loans = {
        SSArchives = false, -- Allow loans only if the player has no dossiers (requires SS-Archives)
        SSIdentityCard = false, -- Require an identity card for loans (requires SS-IdentityCard)
        Jobs = { -- Jobs allowed to take loans
            "Serif", "Maresal", "Judecator", "Guvernator", "PolitiaFederala", "Detectiv",
            "PolitieFrontiera", "VanatorRecompense", "Medic", "Shaman", "Armurier",
            "Miner", "Padurar", "AntrenorCai", "Fierar", "Bijutier", 
            "PrimarBlackWater", "PrimarRhodes"
        },
        Fee = 25, -- Loan fee percentage (e.g., 25% means $1,000 loan requires $1,250 payback)
        PayBacks = 20, -- Percentage deducted per loan installment
        LoanTime = 3, -- Interval (days) for loan repayments
        MaxLoan = 5000, -- Maximum loan amount a player can request
    },

    -- Salary Settings
    SalaryTime = 60, -- Interval (minutes) for salary payouts
    DirectorSalary = 0.5, -- Director salary as a percentage of bank budget (e.g., $20,000 in taxes = $100 salary)

    -- Bank Configurations
    Banks = {
        [1] = {
            Name = "NewHorizon Bank Rhodes", -- Bank Name
            Id = 1, -- Bank ID (used in SS-BankHeist)
            Active = true, -- Enable or disable this bank
            Bank = "Rhodes", -- Internal identifier (do not change)
            Stash = 300, -- Stash slot limit
            Pos = {1292.82, -1304.67, 76.14, -31.90}, -- Bank menu position
            Director = {1288.12, -1309.54, 77.16}, -- Director menu position
            Job = "PrimarRhodes", -- Required job for director
            Npc = "s_m_m_bankclerk_01", -- NPC model (set `false` to disable)
            Blip = -2128054417, -- Blip ID for map marker (`false` to disable)
            Distance = 2.5, -- Interaction distance
        },
        [2] = {
            Name = "NewHorizon Bank Sant Denise",
            Id = 2,
            Active = false,
            Bank = "Saint Denis",
            Stash = 300,
            Pos = {2645.07, -1294.01, 51.35, 21.85},
            Director = {-813.25, -1275.34, 42.74, -174.97},
            Job = "PrimarSaintDenis",
            Npc = "s_m_m_bankclerk_01",
            Blip = -2128054417,
            Distance = 2.5,
        },
        [3] = {
            Name = "NewHorizon Bank Valentine",
            Id = 3,
            Active = true,
            Bank = "Valentine",
            Stash = 300,
            Pos = {-308.01, 773.92, 117.80, 13.64},
            Director = {-308.85, 767.31, 118.49},
            Job = "bankVT",
            Npc = "s_m_m_bankclerk_01",
            Blip = -2128054417,
            Distance = 2.5,
        },
        [4] = {
            Name = "NewHorizon Bank Blackwater",
            Id = 4,
            Active = true,
            Bank = "Blackwater",
            Stash = 300,
            Pos = {-813.34, -1277.52, 43.64, 351.36},
            Director = {-820.71, -1278.61, 43.64, 349.08},
            Job = "bankBW",
            Npc = false,
            Blip = -2128054417,
            Distance = 1.5,
        },
    },
}

-- Notification Function
function NOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000) -- Display notification at the bottom for 5 seconds
end

-- Police Notification
function AlertPolice(bank, coords)
    local coords = {x = coords.x, y = coords.y, z = coords.z}
    local notify = "Notify of an possible FRAUD at Bank"..bank
    local bliptype = 1366733613
    local blipradius = 30.0
    local blipname = "Fraud Bank"
    local blipremove = 10
    exports["SS-PoliceJob"]:PoliceAlert(coords, notify, blipradius, bliptype, blipname, blipremove)
end    
```
{% endcode %}

### config.js

```javascript
TR = {
    loans_tittle: "LOANS REQUESTS",
    all_customers: "CUSTOMERS",
    dir_bank_account: "BANK BUGET",
    dir_salary: "DIRECTOR SALARY",
    trmoneyaccount: "MONEY ACCOUNT",
	trdepositmoney: "DEPOSIT",
    withdrawmoney: "WITHDRAW",
    trgoldaccount: "GOLD ACCOUNT",
	depositgold: "DEPOSIT",
	withdrawgold: "WITHDRAW",
	marketbuygold: "MARKET BUY GOLD",
    buygold: "BUY",
    marketsellgold: "MARKET SELL GOLD",
    sellgold: "SEL",
    unionbankloans: "UNION BANKS LOANS",
    activeloans: "YOUR ACTIVE LOANS",
    askloan: "ASK LOAN",
    wantloan: " wants ",
    loanaccept: "Accept",
    loandecline: "Decline",
    
    //NEW
    checkTittle: "Bank Check Of",
    checkPay: "PAY TO THE ORDER OF: ",
    checkReceive: "INTENDED TO: ",
    checkReceiverInfo: "Name or leave empty for white check",
    checkAmount: "AMOUNT: $",
    checkMemo: "MEMO: ",
    checkDescInfo: "Description of payment...",
    checkSignature: "SIGN HERE",
	checkDate: "DATE:",
    checkDays: "EXPIRE IN:",
    checkExpDays: "DAYS",
    customerInfos: "CUSTOMER FIRSTNAME AND LASTNAME:",
    customerInfoMoney: "CUSTOMER MONEY:",
    customerInfoGold: "CUSTOMER GOLD:",
    customerLoans: "CUSTOMER LOAN:",
    customerPayback: "CUSTOMER PAYBACK:",
    customerTransactions: "CUSTOMER TRANSACTIONS:",
    
    TableFirstname: "Firstname",
    TableLastname: "Lastname",
    TableGold: "Gold",
    TableMoney: "Money",
    TableLock: "Freeze",
    TableUnlock: "Release",
    TableStash: "Stash",
    TableDate: "Date/Time",
    TableAmount: "Amount",
    TableInfo: "Information",
    TableType: "Type",
    backButton: "BACK TO CUSTOMERS",
    
    // CONFIG
    UseHistory: true, // ENABLE Buttons and functions for history of transactions !
    DirectorOpenStash: true, // ALLOW DIRECTOR TO HAVE ACCESS TO STASH OF PEOPLE ?
	MarketGold: 5, // ALTER MARKET GOLD PRICE BY ( / 2) 2 means half price of market price !
    DefaultBuyGold: 17.60, // IF WEBSITE MARKET DOSEN'T RESPOND OR OFFLINE USE DEFAULT
    DefaultSellGold: 15.60, // IF WEBSITE MARKET DOSEN'T RESPOND OR OFFLINE USE DEFAULT
};
```
