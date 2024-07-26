# Configuration File

**Configuration File**

The configuration file defines settings for sending in-game telegrams, including customization options for notifications, jobs that can send official telegrams, webhook integration, date settings, and other parameters.

**Example Configuration**

{% code overflow="wrap" %}
```lua
-- Author 'SIREC' Discord Username
-- REPORT ANY BUGS ON https://discord.gg/9XNBaQSmMd --

Config = {
    Dev = true,  -- USE ONLY ON TEST SERVER FOR CONFIGURATION & TESTS
    Language = "EN",
    SSIdentityCard = true,
    
    OfficialJobs = {"police", "PolitiaFederala"}, -- Official Jobs from which you can send telegrams with job name instead of your name!
    
    Webhook = "", -- Webhook URL for telegram notifications
    WebhookTitle = "NEW TELEGRAM HAS BEEN SENT", -- Title for webhook notifications
    
    CustomDate = "08/1875",  -- Custom date format (Month/Year)
    Use3DCam = false, -- Use 3D camera when calling the telegram
    
    MaxMoneyAmount = 500, -- Maximum amount of money that can be sent via telegram
    
    Telegram = "telegram", -- Item used for sending a telegram
    AnonymousTelegram = "blacktelegram", -- Item for sending an anonymous telegram
    
    Model = "A_C_Eagle_01", -- Bird model for telegram delivery (e.g., A_C_Pigeon)
    ModelAnonymous = "a_c_crow_01", -- Bird model for anonymous telegram delivery
    
    UnlimitedTelegram = false, -- true if you want to send unlimited telegrams with just one item, false to consume one item per telegram
    
    Key = 0xD9D0E1C0, -- Keybind for sending telegrams
    CameraKey = 0x4BC9DABB, -- Keybind for using the 3D camera
    
    TimeCheck = 60, -- Time interval to check for new telegrams (default: 60 seconds)
    ResetTelegram = 600, -- Time to reset the bird telegram if stuck or dead (default: 600 seconds or 10 minutes), "false" to turn off
}

function NOTIFY(text) -- Set your notifications
    TriggerEvent("vorp:TipBottom", text, 5000)
end

```
{% endcode %}

#### Using the Script

1. **Development Mode**: Set `Dev` to `true` for testing and configuration on a test server. Set it to `false` for production.
2. **Language**: Configure the language setting with `Language`.
3. **Identity Card**: Set `SSIdentityCard` to `true` to use identity cards with the telegram system.
4. **Official Jobs**: Define official jobs in `OfficialJobs` array that can send telegrams using the job name instead of the personal name.
5. **Webhook Integration**: Set the `Webhook` URL for telegram notifications and customize the `WebhookTitle`.
6. **Custom Date**: Use the `CustomDate` field to set a custom date format for telegrams.
7. **3D Camera**: Enable the 3D camera with `Use3DCam` when sending telegrams.
8. **Money Transfer**: Configure `MaxMoneyAmount` for the maximum amount of money that can be sent via telegram.
9. **Telegram Items**: Define items used for sending telegrams (`Telegram` and `AnonymousTelegram`).
10. **Bird Models**: Customize bird models for delivering telegrams (`Model` and `ModelAnonymous`).
11. **Unlimited Telegrams**: Set `UnlimitedTelegram` to `true` to send unlimited telegrams with just one item; set it to `false` to consume an item per telegram.
12. **Keybinds**: Define keybinds for sending telegrams (`Key`) and using the 3D camera (`CameraKey`).
13. **Time Intervals**: Configure `TimeCheck` for the interval to check for new telegrams and `ResetTelegram` for resetting the bird telegram if stuck or dead.

#### Final Considerations

This guide covers the basic configuration and use of the SS-Telegram script for RedM. You can further expand the functionality by customizing notifications, integrating with webhooks, and setting up additional official jobs or bird models. If you have any further questions or need assistance, feel free to ask!
