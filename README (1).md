# SS-Crafting

<figure><img src=".gitbook/assets/COVER2.png" alt="" width="563"><figcaption></figcaption></figure>

* [**How to create a receipe ?**](<README (1).md#how-to-create-a-receipe>)
* **Ho to block some receipes on an book/workbench ?**

***

## Create a receipe.

<details>

<summary>Receipe Example</summary>

```
["horsebrush"] = { -- RECEIPE NAME SHOULD BE SAME AS THE ITEM
	Item = "horsebrush", -- ITEM TO RECEIVE
	Amount = 2, -- AMOUNT TO RECEIVE WHEN CRAFTED
	Desc = "help keep your horse's coat clean by removing dust and dirt particles
	 while also giving them a massage which helps release oils that give their 
	coat a glossy shine.", -- ITEM DESCRIPTION AND INFO
	Category = "medic", -- IN WICH CATEGORY SHOULD ADD THE EXP ?
	Level = 0, -- LVL NEED TO CAN CRAFT THIS ITEM
	Exp = 25, -- HOW MUCH EXPERIENCE TO ADD WHEN CRAFT
	isGun = false, -- IS THIS ITEM A GUN ?
	Jobs = {}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
	JobGrades = {}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL ALLOW ANY / {1, 5} WILL BE SHOWED ONLY TO THIS RANK
	SuccessRate = 100, -- % CHANCE TO CRAFT THIS ITEM ?
	Time = 5, -- TIME NEED TO WAIT
        Metadata = {description = "TESTING : ", ["qty"] = 20}, -- ADD METADATA IF YES WICH ? false TURN IT OFF
        Price = 100,
	Ingredients = { -- WHAT INGREDIENTS NEED TO CRAFT THIS RECEIPE
		['bread'] = {amount = 2, returnItem = false, returnAmount = 1},
		['beer'] = {amount = 2, returnItem = false, returnAmount = 1},
	}
},   
```



</details>
