# 📃 Permanent Items

**Permanent items means they may be needed in a recipe but will not be taken. They only require the presence in the inventory to create the recipe, for example for a recipe in which you want to create some nails, you needed an iron and a hammer. The iron will be consumed for the creation of the nails, the exchange of the hammer only requires its presence in the inventory for the creation of the nails, being a permanent object and not consumable.**

***

_**Let's assume that we have this recipe to create nails, in which we have ironbar and hammer as materials. The ironban will be consumed and will disappear from the inventory, instead the hammer will remain and only the presence will be necessary!**_

{% code overflow="wrap" %}
```lua
["nails"] = { -- RECEIPE NAME SHOULD BE SAME AS THE ITEM
		Item = "nails", -- ITEM TO RECEIVE
		Amount = 5, -- AMOUNT TO RECEIVE WHEN CRAFTED
		Desc = "A simple nail !", -- ITEM DESCRIPTION AND INFO
		Category = "tools", -- IN WICH CATEGORY SHOULD ADD THE EXP ?
		Level = 0, -- LVL NEED TO CAN CRAFT THIS ITEM
		Exp = 25, -- HOW MUCH EXPERIENCE TO ADD WHEN CRAFT
		isGun = false, -- IS THIS ITEM A GUN ?
		Jobs = {}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
		JobGrades = {}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL ALLOW ANY / {1, 5} WILL BE SHOWED ONLY TO THIS RANK
		SuccessRate = 100, -- % CHANCE TO CRAFT THIS ITEM ?
		Time = 5, -- TIME NEED TO WAIT
        	Metadata = false, -- ADD METADATA IF YES WICH ? false TURN IT OFF
        	Price = 100,
Ingredients = { -- WHAT INGREDIENTS NEED TO CRAFT THIS RECEIPE
	['ironbar'] = {amount = 2, returnItem = false, returnAmount = 1},
	['hammer'] = {amount = 2, returnItem = false, returnAmount = 1},
	}
},   
```
{% endcode %}

_**In permanent items we have the hammer !**_

{% code overflow="wrap" %}
```lua
PermanentItems = { -- ITEMS THAT JUST NEED TO HAVE IN INVENTORY WILL NOT REMOVE THEM WHEN CRAFTING
["hammer"] = true,
["shovel"] = true,
}, 
```
{% endcode %}
