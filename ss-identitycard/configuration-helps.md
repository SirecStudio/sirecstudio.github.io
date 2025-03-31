# Configuration Helps

#### **General Settings**

* **Dev Mode:** `Dev = true` – Enables debug mode for testing. Set to `false` for production.
* **Language:** `Language = "EN"` – Choose from available language files in `l/l.lua`.
* **Menu Keybind:** `Key = 0xD9D0E1C0` – Defines the key to open the identity menu.
* **Menu Alignment:** `Align = "right"` – Set to `"left"` or `"right"` based on preference.
* **Server Name Display:** `ServerName = "Sirec Studio"` – This text appears on ID cards under the photo.



#### **Identity System Configuration**

* **Identity Card Item Name:** `IdentityCardItem = "identitycard"` – Defines the in-game item name for the ID.
* **Registration Cost:** `PayRegistration = 5` – Cost of registering an ID. Set to `false` to disable.
* **Copy Cost:** `PayCopyRegistration = 1` – Cost for obtaining an additional copy of the ID.
* **Update Info Cost:** `PayInfoUpdate = 1` – Fee for updating details on the ID.
* **Image Upload:** `AllowImageInGame = true` – Enable or disable in-game ID photo updates.

#### **Fake Identity System**

* **Fake ID Item Name:** `FakeIdentityCardItem = "salt"` – Defines the fake ID item name.
* **Fake ID Cost:** `PayFakeId = 250` – Cost of purchasing a fake identity card.
* **Fake Copy Cost:** `PayFakeCopyId = 150` – Cost for obtaining a fake ID copy.
* **Fake ID Restrictions:**
  * `Only1FakeId = false` – If `true`, players can only have **one fake ID** at a time.
  * `PayDeleteFakeId = 1000` – Cost to delete a fake identity from the system.

#### **4. Economy & Police Settings:**

* **Fine Payments to Police:** `SynSociety = "police"` – Determines where fine payments go. Set to `false` to disable.
* **Blacklist Jobs:** `BlackListJobs = {"police", "marshal"}` – These jobs will not appear on ID cards.
* **Replacement for Blacklisted Jobs:** `ReplaceBlackListJobs = "Unemployed"` – If a job is blacklisted, it will show this title instead.
* **Fake ID Default Job:** `FakeIdDefaultJob = "Unemployed"` – Job title that appears on fake IDs.
* **Allowed Police View Access:** `PoliceJobs = false` – Define which jobs can view identity details.

#### **5. National Registration Offices:**

Each registration office has the following settings:

* **City Name:** Displayed on ID as the place of registration.
* **Fake Services:** `FakeServices = true/false` – Determines if an office provides fake IDs.
* **NPC Model & Location:** Configurable NPC for ID services.
* **Blip Display:** Toggle **map blips** for ID offices.

Example of a **National Registration Office**:

{% code overflow="wrap" %}
```lua
[1] = { 
   City = "Valentine",
   FakeServices = false, 
   Name = "Valentine NR Office",
   Desc = "NATIONAL OFFICE",
   NpcModel = "S_M_M_VHTDEALER_01",
   Pos = {-175.2606048584, 631.74407958984, 113.08966064454, 320.85287475586},
   Distance = 3.0,
   Blip = 587827268,
},

```
{% endcode %}
