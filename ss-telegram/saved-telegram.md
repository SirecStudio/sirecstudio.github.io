---
description: REDM SCRIPTS | SIREC STUDIO
---

# Saved telegram

After a new telegram is read, SS-Telegram gives the player a saved telegram item with metadata.

Saved telegrams can be used for roleplay records, evidence, personal letters, contracts, threats, ransom notes, or any other story item your server allows.

***

## How Saved Telegrams Work

1. Player receives and reads a new telegram.
2. The script marks it as read in the database.
3. The script gives the player a telegram item.
4. The item metadata stores the telegram ID.
5. When the item is used later, the script loads the telegram by ID.

***

## Normal & Anonymous Saved Items

Normal telegrams use:

```lua
Telegram = "telegram"
```

Anonymous telegrams use:

```lua
AnonymousTelegram = "blacktelegram"
```

***

## Troubleshooting

If a saved telegram item does not open:

* Check that the item metadata contains `id`.
* Check that the telegram row still exists in `ss_telegram`.
* Check that `SS-Core` registered the usable item.
* Check server console for SQL errors.
