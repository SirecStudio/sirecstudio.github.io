---
description: REDM SCRIPTS | SIREC STUDIO
---

# Send a telegram

Players send telegrams by using the configured telegram item:

```lua
Telegram = "telegram"
```

When the item is used, the telegram bird is called and the write interface opens when the player can interact with it.

***

## Normal Telegrams

Normal telegrams can include:

* Receiver first and last name.
* Sender identity.
* Telegram message.
* Optional money transfer.
* Optional current coordinates.

If `SSIdentityCard = true`, the sender can use identity card data and the receiver can be found through `SS-IdentityCard`.

***

## Anonymous Telegrams

Anonymous telegrams use:

```lua
AnonymousTelegram = "blacktelegram"
```

Anonymous telegrams hide the sender identity from the receiver.

***

## Item Consumption

```lua
UnlimitedTelegram = false
```

If `UnlimitedTelegram = false`, one telegram item is consumed after sending.

If `UnlimitedTelegram = true`, the player can keep using the item without consuming it.

***

## Official Sender Names

Official jobs can send telegrams using the institution/job name:

```lua
OfficialJobs = {"police", "PolitiaFederala"}
```

Use this for sheriff offices, police departments, federal offices, or other roleplay institutions.
