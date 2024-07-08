# 📃 Create a book / workbench

**This is a book and a predefined workbench.**

**Book:**

<pre class="language-lua" data-overflow="wrap"><code class="lang-lua">["medicinebook"] = {
<strong>    Cover = "coverbook",
</strong>    PropSpawn = "p_campfire_coloursmoke01x",
    Animation = {"amb_camp@world_camp_fire_tend_sit@poke_fire@male_a@base", "base"},
    Receipes = {"cigarette"},
},
</code></pre>

Workbench:

<pre class="language-lua" data-overflow="wrap"><code class="lang-lua">[1] = {
    Cover = "coverbook",
    Name = "WorkBench Craft", 
<strong>    Coords = {-2392.17, -2375.76, 60.17, 150.0},
</strong>    Distance = 2.0,
    DrawTxt = "Wood WorkBench",
    SpawnProp = "p_workbench01x", 
    Animation = {"amb_camp@world_camp_fire_tend_sit@poke_fire@male_a@base", "base"}, 
    UseBlip = -758970771, 
    Receipes = {"horsebrush", "boiledegg", "porkcooked", "friedchicken", "scrambledeggsbacon", "fishchips"}, 
    Jobs = {},
    JobsGrades = {},
},      
</code></pre>

***

_Creating a book or workbench is very simple, but we still suggest that they be created after you finish making the recipes. Creating a book is simpler, fewer options._&#x20;

**Cover:** _You can choose the book cover as you wish, you can choose or create one for each category, or as you like. Or you can leave the default "coverbook" cover!_

{% code overflow="wrap" %}
```lua
Cover = "coverbook",
```
{% endcode %}

***

**PropSpawn:** _is the item that you want to be spawned when you open a book, you can choose a prop for each book to identify and express more correctly the craft category or domain. Default is a campfire with quite visible smoke, otherwise it is clear that someone is working and crafting something at the fire._

**Animation:** _you can choose any animation you want the character to do when crafting. {"DICT", "ANIM"}_

{% code overflow="wrap" %}
```lua
PropSpawn = "p_campfire_coloursmoke01x",
Animation = {"amb_camp@world_camp_fire_tend_sit@poke_fire@male_a@base", "base"},
```
{% endcode %}

***



```
// Some code
```
