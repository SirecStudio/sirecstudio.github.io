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



{% code overflow="wrap" %}
```lua
Cover = "coverbook",
```
{% endcode %}
