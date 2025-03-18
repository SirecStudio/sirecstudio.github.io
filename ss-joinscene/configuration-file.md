# Configuration File

{% code overflow="wrap" %}
```lua
-- Author 'SIREC' DISCORD USERNAME
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd --

Config = {
    
Dev = true, -- IF true YOU CAN CHECK THE MAP WITH /testscene / IF false WILL DISABLE IT
UseVideoNewCharacter = true, -- INTRO FOR NEW CHARACTERS ?
SSIdentityCard = false, -- If true any new character will be forced to create an ID before join the server !

UseRejoinScene = true, -- WAKEUP SCENE WHEN JOIN ?
FewMomentLater = "Title_Gen_FewHoursLater",
AiVoiceNewChar = {
	Gender = "M", -- M or F
    Voice = 4, -- VOICES 5 MAX
    Text1 = "Hello ", -- > NAME > TEXT2
    Text2  = ", welcome to Sirec Studio server, this is an example welcome text, but any owner can set his own welcome text. Enjoy you stay...!",
},
    
Cities = {
    [1] = {coords = vector4(-167.455, 631.407, 114.032, 0.0), label = "Valentine", video = "default.mp4"}, --Valentine file or link !
	[2] = {coords = vector4(-798.759, -1205.143, 44.140, 0.0), label = "Blackwater", video = "default.mp4"}, --Annesburg file or link !
    [3] = {coords = vector4(1227.376, -1304.366, 76.904, 0.0), label = "Rhodes", video = "default.mp4"}, --Rhodes file or link !
    [4] = {coords = vector4(2683.544, -1444.589, 46.254, 0.0), label = "Saint Denis", video = "default.mp4"}, --Saint Denis file or link !
	[5] = {coords = vector4(-1776.22, -435.98, 155.00, 0.0), label = "Strawberry", video = "default.mp4"}, --Strawberry file or link !
	[6] = {coords = vector4(2945.909, 1281.752, 44.623, 0.0), label = "Annesburg", video = "default.mp4"}, --Annesburg file or link !
	[7] = {coords = vector4(-3739.4717, -2607.5571, -14.1842, 0.0), label = "Armadillo", video = "default.mp4"}, --Armadillo file or link !
	[8] = {coords = vector4(-5514.7397, -2918.6450, -2.6882, 0.0), label = "Tumbleweed", video = "default.mp4"}, --Tumbleweed file or link !
},
    
}
```
{% endcode %}

