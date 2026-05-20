# Configuration File

## Main Files

SS-Telegram is configured mainly from these files:

* `config.lua`: Main script configuration.
* `l/l.lua`: Lua translations.
* `config.js`: NUI / interface translations.
* `EXTRA/ss_telegram.sql`: SQL for VORP style character IDs.
* `EXTRA/ss_telegram_rsg.sql`: SQL for RSG style character IDs.
* `UI/UI.html`: Telegram UI page.
* `UI/js/js.js`: NUI JavaScript.
* `UI/css/css.css`: NUI styling.

***

## config.lua

{% code overflow="wrap" %}
```lua
Config = {
    Dev = true,
    Language = "EN",
    Key = 0xD9D0E1C0,

    SSIdentityCard = true,
    OfficialJobs = {"police", "PolitiaFederala"},

    Webhook = "",
    WebhookTittle = "NEW TELEGRAM HAS BEEN SENT",

    CustomDate = "08/1875",

    Use3DCam = false,
    CameraKey = 0x4BC9DABB,

    Model = "A_C_Eagle_01",
    ModelAnonymouse = "a_c_crow_01",

    MaxMoneyAmount = 500,

    Telegram = "telegram",
    AnonymousTelegram = "blacktelegram",
    UnlimitedTelegram = false,

    TimeCheck = 60,
    ResetTelegram = 600,
}

function NOTIFY(text)
    TriggerEvent("vorp:TipBottom", text, 5000)
end
```
{% endcode %}

***

## General Settings

```lua
Dev = true
Language = "EN"
Key = 0xD9D0E1C0
```

* `Dev`: Use `true` only while testing. Use `false` on live servers.
* `Language`: Language used by the script.
* `Key`: Prompt key used to call, open, read, and write telegrams.

***

## Optional Integrations

```lua
SSIdentityCard = true
OfficialJobs = {"police", "PolitiaFederala"}
```

* `SSIdentityCard`: Uses `SS-IdentityCard` names and identity data for recipients and sender identities.
* `OfficialJobs`: Jobs allowed to send telegrams using the institution/job name.

If you do not use `SS-IdentityCard`, set:

```lua
SSIdentityCard = false
```

***

## Webhook Settings

```lua
Webhook = ""
WebhookTittle = "NEW TELEGRAM HAS BEEN SENT"
```

* `Webhook`: Discord webhook URL. Leave empty to disable telegram logs.
* `WebhookTittle`: Title used in the Discord log message.

***

## Telegram Date & UI

```lua
CustomDate = "08/1875"
```

* `CustomDate`: Custom month/year printed in telegram text.
* Use `false` if you want the script to use the in-game date flow.

***

## Bird & Camera Settings

```lua
Use3DCam = false
CameraKey = 0x4BC9DABB
Model = "A_C_Eagle_01"
ModelAnonymouse = "a_c_crow_01"
```

* `Use3DCam`: Enables optional 3D camera prompt while calling the bird.
* `CameraKey`: Key used to switch the optional 3D camera.
* `Model`: Bird model for normal telegrams.
* `ModelAnonymouse`: Bird model for anonymous telegrams.

***

## Money & Items

```lua
MaxMoneyAmount = 500
Telegram = "telegram"
AnonymousTelegram = "blacktelegram"
UnlimitedTelegram = false
```

* `MaxMoneyAmount`: Maximum amount of money that can be sent in one telegram.
* `Telegram`: Usable item for normal telegrams.
* `AnonymousTelegram`: Usable item for anonymous telegrams.
* `UnlimitedTelegram`: If `true`, the item is not consumed. If `false`, one item is removed when a telegram is sent.

***

## Timers & Failsafe

```lua
TimeCheck = 60
ResetTelegram = 600
```

* `TimeCheck`: Seconds between checks for unread telegrams.
* `ResetTelegram`: Seconds before a stuck or dead bird is reset. Use `false` to disable the reset.

***

## SQL Tables

Import one SQL file depending on your framework setup:

```text
EXTRA/ss_telegram.sql
EXTRA/ss_telegram_rsg.sql
```

Main tables:

```text
ss_telegram
ss_telegramlist
```

`ss_telegram` stores sent telegrams, receiver data, sender data, message text, money, read state, and optional coordinates.

`ss_telegramlist` stores address book data for saved receiver names.

### Coordinates Column

Current SS-Telegram code writes a `coords` value when coordinate sharing is used. If your database table is old and does not include it, add:

```sql
ALTER TABLE `ss_telegram`
ADD COLUMN `coords` varchar(500) DEFAULT NULL;
```

Run this once after importing the SQL if the column is missing.
