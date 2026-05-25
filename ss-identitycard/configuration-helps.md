# Configuration Helps

## SS-IdentityCard Setup & Configuration Guide

SS-IdentityCard is an identity card system for RedM. It supports real ID cards, fake ID cards, national registration offices, immigration stamps, fines integration, licenses integration, and multiple optional integrations with other Sirec Studio scripts.

This guide is written for server owners who want to install, configure, and test the script safely, even without deep Lua knowledge.

***

## Features Overview

SS-IdentityCard includes:

* Real identity card registration at national registration offices.
* Player information updates after registration.
* Real ID card copies.
* Fake identity card creation, fake copies, and fake ID removal.
* Identity card display for the owner and nearby players.
* Immigration stamp in/out support.
* Fine payment integration.
* Optional integrations with licenses, housing, boats, player shops, train transport, archives, and jobs panel systems.
* Multi-language support.

***

## Dependencies

### Required

* `SS-Core`
* `oxmysql`

### Used By Default

* `menuapi`
* `vorp:TipBottom`, used for notifications.

### Optional Integrations

* `SS-Archives`
* `SS-MedicArchives`
* `SS-Licenses`
* `SS-Housing`
* `SS-PlayerShops`
* `SS-Boats`
* `SS-TrainTransport`
* `SS-Primary`
* `SS-JoinScene`

If you do not use an optional integration, disable it in `config.lua`.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```
resources/[scripts]/SS-IdentityCard
```

Keep the resource folder name exactly:

```
SS-IdentityCard
```

### 2. Import SQL

Import the main SQL file:

```
EXTRA/sql.sql
```

If your existing table is old and does not include immigration or fines fields, also check:

```
EXTRA/imigration.sql
```

The main database table is:

```
ss_identitycard
```

It stores identifier data, character ID, record ID, real and fake identity data, image URL, immigration status, and fines total.

### 3. Start Order

Recommended start order:

```cfg
ensure oxmysql
ensure SS-Core
ensure SS-IdentityCard
```

### 4. Restart The Server

After importing SQL and checking the start order, restart the server and test the registration flow in-game.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main configuration.
* `l/l.lua`: Translations.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.
* `UI/UI.html`: Identity card UI page.

***

## Languages

Languages are configured in:

```
l/l.lua
```

Included languages:

* `EN`
* `IT`
* `ES`
* `FR`
* `DE`
* `PT`
* `RU`
* `RO`

Example:

```lua
Language = "RO"
```

If an invalid language is set, the script falls back to `EN`.

***

## First Configuration

Open:

```
config.lua
```

The file is grouped into clear sections for general settings, card settings, fake ID settings, integrations, offices, registration behavior, and notifications.

### General Settings

```lua
Dev = true
Language = "EN"
Key = 0xD9D0E1C0
Align = "right"
ServerName = "Sirec Studio"
```

* `Dev`: Use `true` while testing. Use `false` on live servers.
* `Language`: Translation language used by the script.
* `Key`: Key used to open office interactions.
* `Align`: Menu alignment, usually `"left"` or `"right"`.
* `ServerName`: Authority or server name displayed on the ID card.

### Real ID Card Settings

```lua
IdentityCardItem = "identitycard"
PayRegistration = 5
PayCopyRegistration = 1
PayInfoUpdate = 1
AllowImageInGame = true
```

* `IdentityCardItem`: Item used to show a real identity card.
* `PayRegistration`: Registration price. Use `false` to make registration free.
* `PayCopyRegistration`: Copy price. Use `false` to make copies free.
* `PayInfoUpdate`: Information update price. Use `false` to make updates free.
* `AllowImageInGame`: Allows players to upload or update their ID image URL in-game.

### Fake ID Settings

```lua
FakeIdentityCardItem = "salt"
PayFakeId = 250
PayFakeCopyId = 150
Only1FakeId = false
PayDeleteFakeId = 1000
```

* `FakeIdentityCardItem`: Usable item for fake identity cards.
* `PayFakeId`: Price for registering a fake ID.
* `PayFakeCopyId`: Price for a fake ID copy.
* `Only1FakeId`: Controls whether players can have only one fake ID at a time.
* `PayDeleteFakeId`: Cost to remove a fake identity.

### Job Privacy Settings

```lua
BlackListJobs = {"police", "marshal"}
ReplaceBlackListJobs = "Unemployed"
FakeIdDefaultJob = "Unemployed"
PoliceJobs = false
```

* `BlackListJobs`: Jobs hidden from the visible ID card.
* `ReplaceBlackListJobs`: Replacement text shown instead of blacklisted jobs.
* `FakeIdDefaultJob`: Job text always shown on fake IDs.
* `PoliceJobs`: Jobs allowed to access protected identity interactions. Use `false` to allow everyone.

***

## Optional Integrations

Only enable integrations for scripts that are actually installed on your server:

```lua
SSMedicArchives = true
SSArchives = true
SSLicenses = true
SSHousing = true
SSPlayerShops = true
SSBoats = true
SSTrainTransport = true
SSPrimary = true
```

If you do not have one of these scripts, set the related option to `false`.

***

## National Registration Offices

Registration offices are configured in:

```lua
Config.NationalRegistration
```

Example:

```lua
[1] = {
    City = "Valentine",
    FakeServices = false,
    Name = "Valentine NR Office",
    Desc = "NATIONAL OFFICE",
    NpcModel = "S_M_M_VHTDEALER_01",
    Pos = {-175.26, 631.74, 113.08, 320.85},
    Distance = 3.0,
    Blip = 587827268,
},
```

Important fields:

* `City`: City printed on IDs registered at this office.
* `FakeServices`: `true` opens fake ID services instead of real ID services.
* `Name`: Office name in the menu or blip.
* `Desc`: Menu subtitle.
* `NpcModel`: NPC model used at the office.
* `Pos`: Office coordinates in `x, y, z, heading` format.
* `Distance`: Interaction range.
* `Blip`: Blip hash or `false`.

### Add A New Office

Copy an existing office and change only the values:

```lua
[6] = {
    City = "Strawberry",
    FakeServices = false,
    Name = "Strawberry NR Office",
    Desc = "NATIONAL OFFICE",
    NpcModel = "S_M_M_VHTDEALER_01",
    Pos = {-1800.0, -350.0, 160.0, 90.0},
    Distance = 3.0,
    Blip = 587827268,
},
```

After adding a new office, restart the resource/server and test the NPC, blip, menu, and registration flow.

***

## Real ID Flow

Real ID registration works like this:

1. The player goes to a real national registration office.
2. The player opens the menu.
3. The player selects register, update, or copy.
4. The UI opens.
5. The script validates age, hair, eyes, height, weight, and payment.
6. The server inserts or updates data in `ss_identitycard`.
7. The identity card item is given to the player.

### Required Registration Data

The registration UI expects:

* First name
* Last name
* Date of birth
* City
* Eye color
* Hair color
* Weight
* Height
* Sex
* Generated record ID

***

## Fake ID Flow

Fake ID registration works like this:

1. The player goes to an office where `FakeServices = true`.
2. The player registers a fake identity.
3. The script checks duplicate names and payment.
4. The server inserts the fake card with `isfake = 1`.
5. The fake identity card item is given to the player.

Fake IDs always show the configured job text from:

```lua
FakeIdDefaultJob = "Unemployed"
```

***

## Immigration Stamp

The script supports an immigration stamp item:

```lua
ImigrationStamp = "stampilabilet"
```

Behavior:

* When another player is showing an ID in stamp mode, the viewer can stamp it.
* Card status changes between `in` and `out`.
* Immigration status is stored in the database.

***

## Fines

If archive integrations are enabled, SS-IdentityCard can:

* Read fines from archive tables.
* Show fines in the menu.
* Let players pay fines.
* Optionally send the money to a society/bank integration.

Related config:

```lua
SSArchives = true
SSMedicArchives = true
SynSociety = "police"
SSBank = false
```

***

## Exports

### Get Your Real ID

```lua
exports["SS-IdentityCard"]:GetIdentityCard()
```

Returns the loaded real ID table, or `false`.

### Get Your Fake ID

```lua
exports["SS-IdentityCard"]:GetIdentityFakeCard()
```

Returns the loaded fake ID table, or `false`.

### Get One ID By Record ID

```lua
exports["SS-IdentityCard"]:GetIdCard(recordid)
```

Returns one identity card from the server, or `false`.

***

## Server Callback Examples

### Get All IDs

```lua
SSCORE.TriggerServerCallback("SS-IDENTITYCARD:SERVER:GETDATA", function(allIds)
    print(allIds)
end)
```

### Get One Specific ID

```lua
SSCORE.TriggerServerCallback("S!r@#Blu$$-SS-ARCHIVES:SERVER:GETIDCARD", function(idCard)
    print(idCard)
end, "K54V86Y73")
```

***

## Manual Register Example

```lua
local info = {
    year = "1855",
    eyes = "blue",
    recordid = "K54V86Y73",
    sex = "M",
    city = "Saint Denis",
    firstname = "Fane",
    lastname = "Baboia",
    kg = "80",
    date = "04-11-1905",
    month = "12",
    dob = "1855-12-11",
    cm = "180",
    hair = "black",
    day = "11"
}

TriggerServerEvent("S!r@#Blu$$-SS-IDENTITYCARD:SERVER:REGISTERID", info)
```

***

## Admin & JoinScene Integrations

SS-IdentityCard also supports these flows:

* Admins can open the registration UI for a player.
* `SS-JoinScene` can open a forced registration UI flow.

These flows are already handled by the script and should not need changes unless you customize the external resources.

***

## Troubleshooting

### Menu Opens But Nothing Happens

Check:

* `menuapi`.
* `SS-Core`.
* Office distance and coordinates.
* NPC and blip config.

### Player Cannot Register

Check:

* Age range settings such as `MinYears` and `MaxYears`.
* Money settings.
* Item names.
* Database table import.

### Card Item Exists But Does Not Show

Check:

* Usable item name in config.
* Metadata `id`.
* Item registration in your inventory/core.

### Image Is Not Visible

Check:

* `AllowImageInGame`.
* Valid image URL.
* UI resource loading correctly.

### Fake ID Menu Should Not Exist

Check offices where:

```lua
FakeServices = true
```

### Fines Do Not Show

Check:

* `SSArchives`.
* `SSMedicArchives`.
* Related archive tables and resources.

***

## Recommended Live Checklist

Before going live, confirm:

* SQL has been imported.
* `SS-Core` starts before `SS-IdentityCard`.
* `Dev = false`.
* `Language` is selected.
* Optional integrations are disabled if missing.
* Item names are checked.
* Real registration office works.
* Fake registration office works.
* ID show/use flow works.
* Immigration stamping works.
* Fine payment works.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature.
* `false` disables a feature.
* Numbers do not use quotes: `100`.
* Item names usually use quotes: `"itemname"`.
* Coordinates usually look like `{x, y, z, heading}`.

Bad:

```lua
PayRegistration = "5"
```

Good:

```lua
PayRegistration = 5
```

Bad, if you do not actually use `SS-Housing`:

```lua
SSHousing = true
```

Good:

```lua
SSHousing = false
```
