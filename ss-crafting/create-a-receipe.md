# 📃 Create a receipe

To create a recipe, you must first have it planned. Add the item you want to be crafted and the items needed to create the recipe in your framework after which you can configure and set the recipe to your liking.

***

Let's assume that we have this recipe to create nails, in which we have ironbar and hammer as materials. The ironban will be consumed and will disappear from the inventory, instead the hammer will remain and only the presence will be necessary!

<pre class="language-lua" data-overflow="wrap"><code class="lang-lua">["<a data-footnote-ref href="#user-content-fn-1">nails</a>"] = { -- RECEIPE NAME SHOULD BE SAME AS THE ITEM
		<a data-footnote-ref href="#user-content-fn-2">Item </a>= "nails", -- ITEM TO RECEIVE
		<a data-footnote-ref href="#user-content-fn-3">Amount </a>= 5, -- AMOUNT TO RECEIVE WHEN CRAFTED
		<a data-footnote-ref href="#user-content-fn-4">Desc </a>= "A simple nail !", -- ITEM DESCRIPTION AND INFO
		<a data-footnote-ref href="#user-content-fn-5">Category </a>= "tools", -- IN WICH CATEGORY SHOULD ADD THE EXP ?
		<a data-footnote-ref href="#user-content-fn-6">Level </a>= 0, -- LVL NEED TO CAN CRAFT THIS ITEM
		<a data-footnote-ref href="#user-content-fn-7">Exp </a>= 25, -- HOW MUCH EXPERIENCE TO ADD WHEN CRAFT
		<a data-footnote-ref href="#user-content-fn-8">isGun </a>= false, -- IS THIS ITEM A GUN ?
		<a data-footnote-ref href="#user-content-fn-9">Jobs </a>= {}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
		<a data-footnote-ref href="#user-content-fn-10">JobGrades </a>= {}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL ALLOW ANY / {1, 5} WILL BE SHOWED ONLY TO THIS RANK
		<a data-footnote-ref href="#user-content-fn-11">SuccessRate </a>= 100, -- % CHANCE TO CRAFT THIS ITEM ?
		<a data-footnote-ref href="#user-content-fn-12">Time </a>= 5, -- TIME NEED TO WAIT
        	<a data-footnote-ref href="#user-content-fn-13">Metadata </a>= false, -- ADD METADATA IF YES WICH ? false TURN IT OFF
        	<a data-footnote-ref href="#user-content-fn-14">Price </a>= 100,
Ingredients = { -- WHAT INGREDIENTS NEED TO CRAFT THIS RECEIPE
	['<a data-footnote-ref href="#user-content-fn-15">ironbar</a>'] = {<a data-footnote-ref href="#user-content-fn-16">amount = 2</a>, <a data-footnote-ref href="#user-content-fn-17">returnItem = false</a>, <a data-footnote-ref href="#user-content-fn-18">returnAmount = 1</a>},
	['<a data-footnote-ref href="#user-content-fn-19">hammer</a>'] = {<a data-footnote-ref href="#user-content-fn-20">amount = 2</a>, <a data-footnote-ref href="#user-content-fn-21">returnItem = false</a>, <a data-footnote-ref href="#user-content-fn-22">returnAmount = 1</a>},
	}
},   
</code></pre>

Here you must set the item you want to be crafted, and which you want the player to receive after finishing crafting the recipe!

{% code overflow="wrap" %}
```lua
PermanentItems = {
    ["hammer"] = true,
    ["shovel"] = true,
}, 
```
{% endcode %}

Here you must set the item you want to be crafted, and which you want the player to receive after finishing crafting the recipe!

{% code overflow="wrap" %}
```lua
    ["itemcrafted"] = { -- RECEIPE NAME SHOULD BE SAME AS THE ITEM
        Item = "itemcrafted", -- ITEM TO RECEIVE
```
{% endcode %}

Here you have to set the amount you want the player to receive after finishing crafting the recipe.

{% code overflow="wrap" %}
```lua
        Amount = 2, -- AMOUNT TO RECEIVE WHEN CRAFTED
```
{% endcode %}

Here are the information and description of the recipe such as the description of the item, its category which can be EX: doctor, tools, furniture etc etc, the level required to create this recipe and the experience it gives when finishing the craft..

{% code overflow="wrap" %}
```lua
Desc = "description", -- ITEM DESCRIPTION AND INFO
Category = "medic", -- IN WICH CATEGORY SHOULD ADD THE EXP ?
Level = 0, -- LVL NEED TO CAN CRAFT THIS ITEM
Exp = 25, -- HOW MUCH EXPERIENCE TO ADD WHEN CRAFT
```
{% endcode %}

If the item is a weapon you will have to set true, if it is only an item you will have to set false.

{% code overflow="wrap" %}
```lua
isGun = false, -- IS THIS ITEM A GUN ?
```
{% endcode %}

If this recipe requires a specific job or a specific degree, you will have to set the required job and degree, those who do not have this job or degree will not be able to craft this recipe even if they have the necessary materials and experience.

{% code overflow="wrap" %}
```lua
// FOR NO JOBS & GRADE 
Jobs = {}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
JobGrades = {}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL 
// FOR JOB OR GRADE
Jobs = {"police}, -- WHAT JOBS CAN CRAFT THIS ITEM ? {} WILL ALLOW ANYBODY / {"jobname, "jobname"} WILL BE SHOWED ONLY TO THEM
JobGrades = {2, 3, 10}, -- WHAT JOBS GRADE CAN CRAFT THIS ITEM ? {} WILL 
```
{% endcode %}

If you want this recipe to be crafted without problems and you can always set it to 100%, if you want the probability of crafting to be difficult and to fail, set the probability of success.

{% code overflow="wrap" %}
```lua
    SuccessRate = 100, -- % CHANCE TO CRAFT THIS ITEM ?
    Time = 5, -- TIME NEED TO WAIT
```
{% endcode %}

Some frameworks accept metadata for items, which you can set directly here, and upon completion of the craft, that item will already have predefined metadata.

{% code overflow="wrap" %}
```lua
    Metadata = {description = "TESTING : ", ["qty"] = 20},
```
{% endcode %}

Here you will have to set the necessary materials (items) for crafting this recipe, any desired materials can be added. A material can return another material after its use, if yes, set which and how many. A good example is to suppose that you need a bottle of water, you set the water bottle as an item and on return you can set an empty bottle.

{% code overflow="wrap" %}
```lua
    Ingredients = { -- WHAT INGREDIENTS NEED TO CRAFT THIS RECEIPE
        ['bread'] = {amount = 2, returnItem = false, returnAmount = 1},
        ['beer'] = {amount = 2, returnItem = false, returnAmount = 1},
    }
```
{% endcode %}

[^1]: Items to be crafter and receipe name !

[^2]: Item to receive when craft finish !

[^3]: How many to receive

[^4]: Description of the item to show in the book !

[^5]: From wich category is this item ?

[^6]: From wich level can be crafted ?

[^7]: How many EXP to give when craft finish ?

[^8]: Is a gun or item ?

[^9]: Block this receipe for some jobs ?

[^10]: Block this receipe for some grades of jobs ?

[^11]: Success to finish the craft

[^12]: How many seconds to wait ?

[^13]: Choice metadata for this item.

[^14]: Need to pay for this receipe ?

[^15]: Item to take !

[^16]: Amount to take

[^17]: What item should return? item/false

[^18]: Amount the of the returned item !

[^19]: Item to take !

[^20]: Amount to take

[^21]: What item should return? item/false

[^22]: Amount the of the returned item !
