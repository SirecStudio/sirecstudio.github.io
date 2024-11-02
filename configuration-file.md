# Configuration File



{% code overflow="wrap" %}
```lua
-- Author 'SIREC' Discord Username !
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd --

Config = {
WebHook = "", -- FOR LOGS
    
Dev = true, -- DEV true FOR TESTING SERVER / false FOR MAIN SERVER !
Language = "RO", -- LANGUAGE (CHECK l/l.lua FOR LANGUAGES)
    
BankButton = 0x760A9C6F, -- OPEN BANK BUTTON
SecurityButton = 0x9959A6F0, -- OPEN SECURITY STASH BUTTON
ExchangeButton = 0xD9D0E1C0, -- EXCHANGE BUTTON
CanLock = true, -- CAN DIRECTOR FREEZE PLAYERS ACCOUNT ?
    
GoldBarItem = "goldbar", -- GOLD BAR ITEM FOR EXCHANGE
UseTax = true, -- USE TAX PLAYERS ? 
TaxTime = 7, -- EVERY HOW MANY DAYS TO TAKE TAXES
TaxPrice = 1, -- % TAX ( 1% IS LIKE 500$ from 50.000$ )
    
TaxWithdraw = 1, -- TAX $ PLAYER ON WITHDRAW ORDER !
TaxDeposit = 1, -- TAX $ PLAYER ON DEPOSIT ORDER !
BlacklistItems = {"cigarette", "weed_leaves", "heroin", "opium", "morphine", "cigar", "joint", "weedbags", "hashish", "lockpick", "ammodynamite", "smallbomb", "bigbomb", "ammopoisonbottle", "handcuffs", "handcuffskey", "typhus_injection"}, -- false TO DISABLE / TABLE WITH ITEMS FOR ENABLE {"item", "item", "item"} !
    
Loans = {
	--MinHours = 0, -- ALLOW LOAN ONLY IF PLAYER HAS OVER THIS HOURS ?
	SSArchives = true, -- ALLOW LOAN ONLY IF PLAYER HAS NO DOSSIERS ? Active it only if you have SS-Archives
	SSIdentityCard = true, -- ALLOW LOAN ONLY IF PLAYER HAS IDENTITY CARD ? Active it only if you have SS-IdentityCard
	Jobs = {"Serif", "Maresal", "Judecator", "Guvernator", "PolitiaFederala", "Detectiv", "PolitieFrontiera", "VanatorRecompense", "Medic", "Shaman", "Armurier", "Miner", "Padurar", "AntrenorCai", "Fierar", "Bijutier", "PrimarBlackWater", "PrimarRhodes"}, -- WHO CAN TAKE LOANS ?
        
    Fee = 25, -- HOW MUCH THE PLAYER MUST PAYBACK % ? (25 means 250$ is he ask 1000$ loan)
	PayBacks = 20, -- HOW MUCH TO TAKE % EVERY LoanTime FROM PLAYER ?
	LoanTime = 3, -- EVERY HOW MANY DAYS TO TAKE MONEY FOR LOANS ?
    MaxLoan = 5000, -- MAX LOAN A PLAYER CAN ASK
},

SalaryTime = 60, -- EVERY HOW MUCH MINUTES TO RECIVE SALARY ?
DirectorSalary = 0.5, -- DIRECTOR SALARY % OF BANK BUGET ( If bank has 20.000 COLECTED FROM TAXES AND LOANS, will be 100$ Salary)
    
Banks = {
[1] = {
	Name = "Banca Rhodes Union", -- UNIQUE BANK NAME
    Id = 1, -- BANK ID FROM SS-BankHeist BANK !
	Active = true,
    Bank = "Rhodes",  -- DON'T TOUCH
    Stash = 300,
	Pos = {1292.8172607421875, -1304.6746826171875, 76.14263916015625, -31.899}, --POSITION BANK MENU
	Director = {1288.11767578125, -1309.5369873046875, 77.16206359863281}, --POSITION BANK MENU
    Job = "PrimarRhodes",
	Npc = "s_m_m_bankclerk_01", -- USE NPC ?
    Blip = -2128054417, -- USE BLIP ? false FOR DISABLE
	Distance = 2.5, -- DISTANCE FROM MENU TO SHOW ?
},
[2] = {
	Name = "Banca Saint Denis Union", -- UNIQUE BANK NAME
    Id = 2, -- BANK ID FROM SS-BankHeist BANK !
	Active = true,
    Bank = "Saint Denis", -- DON'T TOUCH
    Stash = 300,
	Pos = {2645.073974609375, -1294.0125732421875, 51.34748458862305, 21.848}, --POSITION BANK MENU
	Director = {-813.246337890625, -1275.343017578125, 42.73772811889648, -174.967}, --POSITION BANK MENU
    Job = "PrimarSaintDenis",
	Npc = "s_m_m_bankclerk_01", -- USE NPC ?
    Blip = -2128054417, -- USE BLIP ? false FOR DISABLE
	Distance = 2.5, -- DISTANCE FROM MENU TO SHOW ?
},
[3] = {
	Name = "Banca Valentine Union", -- UNIQUE BANK NAME
    Id = 3, -- BANK ID FROM SS-BankHeist BANK !
	Active = true,
    Bank = "Valentine",  -- DON'T TOUCH
    Stash = 300,
	Pos = {-308.0148010253906, 773.916015625, 117.80313873291016, 13.642}, --POSITION BANK MENU
	Director = {-308.8492431640625, 767.3116455078125, 118.49244689941406}, --POSITION BANK MENU
    Job = "PrimarValentine",
	Npc = "s_m_m_bankclerk_01", -- USE NPC ?
    Blip = -2128054417, -- USE BLIP ? false FOR DISABLE
	Distance = 2.5, -- DISTANCE FROM MENU TO SHOW ?
},
[4] = {
	Name = "Banca Blackwater Union", -- UNIQUE BANK NAME
	Id = 4, -- BANK ID FROM SS-BankHeist BANK !
	Active = true,
    Bank = "Blackwater",  -- DON'T TOUCH
    Stash = 300, -- STASH SLOT LIMIT
	Pos = {-813.3378 , -1277.5221 , 43.6377 , 351.3564}, -- POSITION BANK MENU
	Director = {-820.7080 , -1278.6130 , 43.6380 , 349.0783}, -- POSITION BANK MENU
    Job = "Guvernator",
	Npc = false, -- USE NPC ?
    Blip = -2128054417, -- USE BLIP ? false FOR DISABLE
	Distance = 1.5, -- DISTANCE FROM MENU TO SHOW ?
},
},
}

function NOTIFY(text) --SET YOUR NOTIFYCATIONS
	TriggerEvent("vorp:TipBottom", text, 5000)   
end
```
{% endcode %}
