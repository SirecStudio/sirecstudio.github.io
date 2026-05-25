---
description: SS-Weapons documentation
---

# SS-Weapons

<figure><img src=".gitbook/assets/weapons preview1.png" alt=""><figcaption></figcaption></figure>

**Overview**

**SS-Weapons** is a complete RedM weapon store, ammo, gunsmith, weapon customization, weapon condition, repair, cleaning, HUD, and preview system.

The script lets server owners configure weapon stores, gunsmith benches, weapon and ammo catalogs, custom weapon serials and labels, component editing, saved gunsmith templates, weapon dirt/soot/damage/permanent wear, cleaning through the native inspection flow, repair kits, ammo box usage, and optional poison/tranquilizer effects.

* **Weapon & Ammo Store System**
  * Players can buy weapons and ammo from configured stores.
  * Stores can sell all configured items or only selected weapons/ammo.
  * Custom serials and custom labels can be enabled per store.
* **Gunsmith System**
  * Configured gunsmith benches allow supported weapons to be edited.
  * Supports component, material, engraving, engraving material, tint, scope, grip, wrap, body, barrel, sight, trigger, hammer, cylinder, clip, and skin pricing.
  * Gunsmith access can be limited by job.
* **Weapon Templates**
  * Players can save a gunsmith setup as a template.
  * Templates can be applied again later or deleted.
  * Templates are saved per owner, character, weapon, and template name.
* **Weapon Wear, Cleaning & Repair**
  * Saves dirt, soot, condition, damage, and permanent rust/wear.
  * Cleaning uses the native weapon inspection flow.
  * Repair kits can reduce permanent rust/damage.
  * Weapons can be blocked from use when permanent degradation reaches the configured limit.
* **Weapon HUD & Preview**
  * Optional weapon HUD with weapon image and ammo display.
  * Gunsmith preview weapons can be synchronized to nearby players.
  * Weapon and ammo images are loaded from the NUI assets.
* **Catalog Data**
  * Includes 57 weapon entries in `cfg/weapons.lua`.
  * Includes 44 ammo entries in `cfg/ammo.lua`.
  * Supports category-based UI browsing.
* **Multi-Language Support**
  * Includes language support for `EN`, `IT`, `ES`, `FR`, `DE`, `PT`, `RU`, and `RO`.
