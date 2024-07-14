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
