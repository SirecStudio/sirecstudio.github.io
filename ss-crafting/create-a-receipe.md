# 📃 Create a receipe

To create a recipe, you must first have it planned. Add the item you want to be crafted and the items needed to create the recipe in your framework after which you can configure and set the recipe to your liking.

***

_This is what a predefined recipe looks like._

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

***

Here you must set the item you want to be crafted, and which you want the player to receive after finishing crafting the recipe!

```lua
	["itemcrafted"] = { -- RECEIPE NAME SHOULD BE SAME AS THE ITEM
		Item = "itemcrafted", -- ITEM TO RECEIVE
```

***

Here you have to set the amount you want the player to receive after finishing crafting the recipe.

```lua
		Amount = 2, -- AMOUNT TO RECEIVE WHEN CRAFTED
```

***

Here are the information and description of the recipe such as the description of the item, its category which can be EX: doctor, tools, furniture etc etc, the level required to create this recipe and the experience it gives when finishing the craft..

```lua
Desc = "description", -- ITEM DESCRIPTION AND INFO
Category = "medic", -- IN WICH CATEGORY SHOULD ADD THE EXP ?
Level = 0, -- LVL NEED TO CAN CRAFT THIS ITEM
Exp = 25, -- HOW MUCH EXPERIENCE TO ADD WHEN CRAFT
```

***

If the item is a weapon you will have to set true, if it is only an item you will have to set false.

```lua
isGun = false, -- IS THIS ITEM A GUN ?
```

***

If this recipe requires a specific job or a specific degree, you will have to set the required job and degree, those who do not have this job or degree will not be able to craft this recipe even if they have the necessary materials and experience.

<pre class="language-lua"><code class="lang-lua"><strong>// FOR NO JOBS &#x26; GRADE 
</strong><strong>Jobs = {}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
</strong>JobGrades = {}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL 
// FOR JOB OR GRADE
<strong>Jobs = {"police}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
</strong>JobGrades = {2, 3, 10}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL 
</code></pre>

***

If you want this recipe to be crafted without problems and you can always set it to 100%, if you want the probability of crafting to be difficult and to fail, set the probability of success.

```lua
SuccessRate = 100, -- % CHANCE TO CRAFT THIS ITEM ?
Time = 5, -- TIME NEED TO WAIT
```

***

Some frameworks accept metadata for items, which you can set directly here, and upon completion of the craft, that item will already have predefined metadata.

{% code overflow="wrap" %}
```lua
Metadata = {description = "TESTING : ", ["qty"] = 20}, -- ADD METADATA IF YES WICH ? false TURN IT OFF
```
{% endcode %}

***

Here you will have to set the necessary materials (items) for crafting this recipe, any desired materials can be added. A material can return another material after its use, if yes, set which and how many. A good example is to suppose that you need a bottle of water, you set the water bottle as an item and on return you can set an empty bottle.

```lua
	Ingredients = { -- WHAT INGREDIENTS NEED TO CRAFT THIS RECEIPE
		['bread'] = {amount = 2, returnItem = false, returnAmount = 1},
		['beer'] = {amount = 2, returnItem = false, returnAmount = 1},
		}
```
