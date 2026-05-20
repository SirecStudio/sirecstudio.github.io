---
description: REDM SCRIPTS | SIREC STUDIO
---

# Receive a telegram

SS-Telegram checks for unread telegrams on a configured interval:

```lua
TimeCheck = 60
ResetTelegram = 600
```

When a new telegram exists, the player receives a notification and the bird delivery flow starts.

***

## Delivery Flow

1. The script detects an unread telegram.
2. The player is notified.
3. A bird flies above the player.
4. The player calls the bird down when ready.
5. The telegram opens in the read interface.
6. The telegram is saved as an inventory item.
7. The database row is marked as read.

This avoids forcing the telegram open during combat, roleplay scenes, interiors, or other bad timing.

***

## Coordinate Telegrams

If the telegram includes coordinates, the receiver can see a location reference and temporary map route.

The database must include:

```sql
ALTER TABLE `ss_telegram`
ADD COLUMN `coords` varchar(500) DEFAULT NULL;
```

***

## Money Telegrams

If the telegram includes money, the receiver gets the money when reading the new telegram.

Old saved telegram items should not pay the money again after the first read.
