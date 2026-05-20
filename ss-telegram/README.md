---
description: SS-Telegram documentation
---

# SS-Telegram

<figure><img src="../.gitbook/assets/ss-telegram-paper.png" alt=""><figcaption></figcaption></figure>

## Overview

**SS-Telegram** is a RedM telegram system built around immersive bird delivery, NUI telegram writing, saved telegram items, anonymous messages, money transfers, location sharing, and optional `SS-IdentityCard` integration.

The script lets players send roleplay telegrams by name, receive unread telegrams through a delivery bird flow, keep old telegrams as inventory items, and use real, fake, or official institution identities when the identity card integration is enabled.

## Main Features

* **Telegram Sending**
  * Players can send telegrams to other players by first and last name.
  * Supports normal telegrams and anonymous telegrams.
  * Supports optional money transfer inside a telegram.
  * Supports optional sender coordinates with a temporary map blip and GPS route.
* **Telegram Receiving**
  * The script checks for unread telegrams on a configurable interval.
  * New telegrams are delivered through a bird flow.
  * Players can call the bird down when they are ready to read the telegram.
  * The telegram is marked as read after it is collected.
* **Saved Telegram Items**
  * Received telegrams are saved back into the player inventory as item metadata.
  * Old telegram items can be read again later.
  * Saved telegrams can be used as roleplay evidence or shared with other players.
* **Anonymous Telegrams**
  * Anonymous telegrams use a separate item.
  * Sender identity is hidden from the receiver.
  * Anonymous telegrams use a separate bird model.
* **SS-IdentityCard Integration**
  * Uses real identity names, fake identity names, and official job/institution names.
  * Recipient search can use identity card data when enabled.
  * Official jobs can send telegrams as the job/institution name.
* **Multi-Language Support**
  * Includes language support for `EN`, `IT`, `ES`, `FR`, `DE`, `PT`, `RU`, and `RO`.
  * Supports both Lua notification text and UI text.
