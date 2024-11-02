# Configuration File



```lua
-- Author Sirec Studio -- 
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd --

Config = {
    
SSBank = true, -- true IF YOU HAVE SS-Bank AND GET THE WIN TICKET IN INVENTORY AS ITEM AND REDEEM IT AT BANK / false TO GET PRIZE INSTANTLY !    
    
Tickets = {
    ["luckyticket"] = { -- BRONZE TICKET
		[1] = {
			Prize = 1, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 15, -- % OF CHANCE
		},
		[2] = {
			Prize = 5, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 10, -- % OF CHANCE
		},
		[3] = {
			Prize = 25, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 5, -- % OF CHANCE
		},
		[4] = {
			Prize = "goldbar", -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 3, -- % OF CHANCE
		},
	},
    ["luckyticket2"] = { -- SILVER TICKET
		[1] = {
			Prize = 5, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 15, -- % OF CHANCE
		},
		[2] = {
			Prize = 25, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 10, -- % OF CHANCE
		},
		[3] = {
			Prize = 50, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 5, -- % OF CHANCE
		},
		[4] = {
			Prize = "silverbar", -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 3, -- % OF CHANCE
		},
	},
    ["luckyticket3"] = { -- GOLD TICKET
		[1] = {
			Prize = 25, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 15, -- % OF CHANCE
		},
		[2] = {
			Prize = 50, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 10, -- % OF CHANCE
		},
		[3] = {
			Prize = 100, -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 5, -- % OF CHANCE
		},
		[4] = {
			Prize = "goldbar", -- NUMBER FOR MONEY (EX: 10,) - ITEMNAME FOR ITEM (EX: "chocolate")
            Chance = 3, -- % OF CHANCE
		},
	},
},

Translate = {
	["youwin"] = "WIN PRIZE: ",
	['winnotifybank'] = 'You win, redeem the prize at any Bank, Prize: ',
	['winnotify'] = "CONGRATS !, From this ticket you win ",
	['youlose'] = 'TRY AGAIN, MAYBE MORE LUCK NEXT TIME...',
	["notnearbank"] = "REDEEM this ticket at any Bank !",
	['winonticket'] = '💲 ! CONGRATS !💲',
	['loseonticket'] = '❌ ! YOU LOSE ! ❌',
	['scratchInfo'] = 'Scratch with the cursor, remember to scratch it to the end! ',
	},
}    

function NOTIFY(text) --SET YOUR NOTIFICATIONS
	TriggerEvent("vorp:TipBottom", text, 5000) 
end 
```
