# Configuration File

{% code overflow="wrap" %}
```lua
-- Author 'SIREC' (DISCORD USERNAME)
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd

Config = {
    Dev = true, -- Put true to check info in F8 when restart script in GAME!
    Language = "EN", -- CHOICE LANGUAGE SEE l/l.lua !
    Key = 0xD9D0E1C0, -- KEY TO OPEN MENU
    Align = "right", -- ALIGN MENU
    NXTInventory = false, -- if you have NXTInventory!
    ServerName = "Sirec Studio", -- WILL BE THE SIGN ON IDENTITY CARD UNDER PHOTO
    
    WebHook = "", -- FOR LOGS
    WebHookInfo = "HAS REGISTERED HIS IDENTITY CARD ID WITH NR",
    WebHookUpdate = "HAS UPDATED HIS IDENTITY CARD",

    -- ADDONS
    ImigrationStamp = "stampilabilet", -- STAMP IN/OUT IMIGRATION OFFICE
    SSMedicArchives = true,
    SSArchives = true, -- PUT true TO MAKE PEOPLE PAY FINES / false IF YOU DON'T HAVE SS-ARCHIVES
    SSLicenses = true, -- PUT true IF YOU HAVE SS-Licenses / false IF YOU DON'T HAVE
    SSHousing = true, -- PUT true IF YOU HAVE SS-Housing / false IF YOU DON'T HAVE
    SSPlayerShops = true, -- PUT true IF YOU HAVE SS-PlayerShops / false IF YOU DON'T HAVE
    SSBoats = true, -- PUT true IF YOU HAVE SS-Boats / false IF YOU DON'T HAVE
    SSTrainTransport = true, -- PUT true IF YOU HAVE SS-TrainTransport / false IF YOU DON'T HAVE
    SSPrimary = true, -- PUT true IF YOU HAVE SS-Primary / false IF YOU DON'T HAVE
    
    -- IDENTITY CARD CONFIG
    IdentityCardItem = "identitycard", -- ITEM NAME OF IDENTITY CARD TO USE
    PayRegistration = 5, -- TURN OFF WITH false OR INSERT PRICE OF IDENTITY CARD   
    PayCopyRegistration = 1, -- TURN OFF WITH false OR INSERT PRICE OF IDENTITY CARD WHEN ASK FOR COPY
    PayInfoUpdate = 1, -- TURN OFF WITH false OR INSERT PRICE FOR CHANGING IDENTITY CARD INFOS
    AllowImageInGame = true, -- TURN ON TO ALLOW PEOPLE UPLOAD/UPDATE IMAGES IN-GAME

    FakeIdentityCardItem = "salt", -- ITEM NAME OF FAKE IDENTITY CARD TO USE
    PayFakeId = 250, -- TURN OFF WITH false OR INSERT PRICE OF IDENTITY CARD
    PayFakeCopyId = 150, -- TURN OFF WITH false OR INSERT PRICE OF IDENTITY CARD WHEN ASK FOR FAKE COPY
    Only1FakeId = false, -- IF true, the players can't delete their fake ID to make a new one! false they can delete and make a new fake id unlimited!
    PayDeleteFakeId = 1000, -- TURN OFF WITH false OR INSERT PRICE TO DELETE IDENTITY CARD

    SynSociety = "police", -- WHERE TO GO THE MONEY FROM FINES? PUT THE JOB OR false TO TURN OFF
    SSBank = false, -- DON'T USE FOR MOMENT SS-Bank WILL BE RELEASED SOON!
    BlackListJobs = {"police", "marshal"}, -- What job's to don't show in IDENTITY CARD?
    ReplaceBlackListJobs = "Unemployed", -- WHAT TO SHOW IF JOB ARE BLACKLISTED?
    FakeIdDefaultJob = "Unemployed", -- What job to show on FAKE IDENTITY JOB?

    ServerYear = 1905, -- ID CARDS WILL BE RELEASED IN THIS YEAR
    MaxYears = 80, -- THE MAX YEARS A PLAYER CAN HAVE
    MinYears = 18, -- THE MIN YEARS A PLAYER CAN HAVE
    PoliceJobs = false, -- {"police", "marshall"}, -- WHO CAN VIEW OTHERS ID CARD INFO? ADD JOBS FOR SOME OR false FOR EVERYONE

    UseAnimProp = true, -- DO ANIMATION AND PROP WHEN SHOW THE IDENTITY CARD

    NationalRegistration = {
        [1] = { 
            City = "Valentine", -- CITY NAME WILL SHOW ON ID WHERE WAS REGISTERED PUT ONLY CITY NAME
            FakeServices = false, -- PROVIDE FAKE SERVICES
            Name = "Valentine NR Office", -- BLIP NAME AND TITLE MENU
            Desc = "NATIONAL OFFICE", -- SUBMENU DESCRIPTION   
            NpcModel = "S_M_M_VHTDEALER_01", -- NPC MODEL
            Pos = {-175.2606048584, 631.74407958984, 113.08966064454, 320.85287475586}, -- POS NPC/BLIP
            Distance = 3.0, -- DISTANCE TO OPEN MENU
            Blip = 587827268, -- Blip model or false to hide
        },
        [2] = { 
            City = "Blackwater",
            FakeServices = false,              
            Name = "BlackWater NR Office",
            Desc = "NATIONAL OFFICE",     
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {-762.0810546875, -1272.1394042968, 43.050540924072, 86.552299499512},
            Distance = 3.0,
            Blip = 587827268,
        },  
        [3] = { 
            City = "Rhodes",
            FakeServices = false,
            Name = "Rhodes NR Office",
            Desc = "NATIONAL OFFICE",      
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {1230.1987304688, -1298.5638427734, 75.904258728028, 232.19049072266},
            Distance = 3.0,
            Blip = 587827268,
        },         
        [4] = { 
            City = "Saint Denis",
            FakeServices = false,
            Name = "Saint Denis NR Office",
            Desc = "NATIONAL OFFICE",    
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {2747.9025878906, -1396.4379882812, 46.183067321778, 24.291278839112},
            Distance = 3.0,
            Blip = 587827268,
        },
        [5] = { 
            City = "Saint Denis",
            FakeServices = true,            
            Name = "Mrs Thomson",
            Desc = "NATIONAL OFFICE",     
            NpcModel = "S_M_M_VHTDEALER_01",
            Pos = {2859.19140625, -1202.2645263672, 48.590869903564, 1.381891965866},
            Distance = 3.0,
            Blip = false,
        },         
    },
}

function NOTIFY(text) -- SET YOUR NOTIFICATIONS
    TriggerEvent("vorp:TipBottom", text, 5000)       
end  

--[[
#####################-DEV CONFIG-#####################
CLIENT EXPORTS

1) exports["SS-IdentityCard"]:GetIdentityCard() | GET YOUR IDENTITY CARD (return all identity card info / false)

2) exports["SS-IdentityCard"]:GetIdCard(recordid) | GET IDENTITY CARD BY ID NR )

3) SSCORE.TriggerServerCallback(("SS-IDENTITYCARD:SERVER:GETDATA", function(allIds) -- RETURN ALL ID CARDS

end)

4) SSCORE.TriggerServerCallback(("S!r@#Blu$$-SS-ARCHIVES:SERVER:GETIDCARD", function(allIds) -- RETURN SPECIFIED ID CARD

end, idcard)

REGISTER THROUGH TRIGGER SENDING THESE INFORMATION 
local info = {year = "1855", eyes = "blue", recordid = "K54V86Y73", sex = "M", city = "Saint Denis", firstname = "Fane", lastname = "Baboia", kg = "80", date = "04-11-1905", month = "12", dob = "1855-12-11", cm = "180", hair = "black", day = "11"}
TriggerServerEvent("S!r@#Blu$$-SS-IDENTITYCARD:SERVER:REGISTERID", info)

]]

```
{% endcode %}

