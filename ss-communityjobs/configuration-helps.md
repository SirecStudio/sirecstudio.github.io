# Configuration Helps

## SS-CommunityJobs Setup & Configuration Guide

SS-CommunityJobs is a community jobs and forced labor script for RedM. It supports city job offices, one-step work tasks, carry jobs, salary tracking, fine reduction, forced labor integration, and optional menu systems.

This guide is written for server owners who want to install, configure, and test the script safely, even without deep Lua knowledge.

***

## Features Overview

SS-CommunityJobs includes:

* City-based community jobs menu.
* Multiple work types per city office.
* One-step jobs such as broom and windows.
* Two-step carry jobs with pickup and delivery flow.
* Server-side salary tracking until withdrawal.
* Forced labor reduction through `SS-Archives`.
* Fine reduction before cash payment.
* External opening from scripts such as `SS-IdentityCard`.
* Multi-language support.

***

## Dependencies

### Required

* `SS-Core`
* `oxmysql`

### Used By Default

* `MNotify`
* `SS-ProgressBar`

### Menu Support

* `SS-Menu` if `Config.SSMenu = true`.
* `vorp_menu` / `menuapi` if `Config.SSMenu = false`.

### Optional Integrations

* `SS-Archives`
* `SS-IdentityCard`

If you do not use an optional integration, disable it in `config.lua`.

***

## Installation

### 1. Add The Resource

Place the script in your server resources folder:

```text
resources/[scripts]/SS-CommunityJobs
```

Keep the resource folder name exactly:

```text
SS-CommunityJobs
```

### 2. Check Start Order

Recommended start order:

```cfg
ensure oxmysql
ensure SS-Core
ensure MNotify
ensure SS-ProgressBar
ensure SS-Menu
ensure SS-CommunityJobs
```

If you use `vorp_menu` instead of `SS-Menu`, make sure `menuapi` is started before this resource and set:

```lua
SSMenu = false
```

### 3. Optional Integrations

If your server uses `SS-Archives` and `SS-IdentityCard`, make sure they are started too:

```cfg
ensure SS-Archives
ensure SS-IdentityCard
```

### 4. Restart The Server

After checking your config and start order, restart the server and test the main job flow in-game.

***

## Main Files

* `fxmanifest.lua`: Resource manifest.
* `config.lua`: Main configuration.
* `l/l.lua`: Translations.
* `c/c.lua`: Client logic.
* `s/s.lua`: Server logic.

***

## Languages

Languages are configured in:

```text
l/l.lua
```

Included languages:

* `EN`
* `RO`
* `IT`
* `DE`
* `FR`
* `ES`
* `PT`

Example:

```lua
Language = "RO"
```

If an invalid language is selected, the script automatically falls back to `EN`.

***

## First Configuration

Open:

```text
config.lua
```

The file is grouped into clear sections so you can configure it safely without touching code logic.

### General Settings

```lua
Language = "EN"
SSMenu = true
Align = "right"
```

* `Language`: Translation language used by the script.
* `SSMenu`: `true` uses `SS-Menu`; `false` uses `vorp_menu` / `menuapi`.
* `Align`: Menu alignment.

### Keybind Settings

```lua
WorkButton = 0x8AAA0AD4
StopButton = 0x760A9C6F
EnterExitPassenger = 0x760A9C6F
RentBallon = 0x8AAA0AD4
BallonRoutes = 0x760A9C6F
```

* `WorkButton`: Prompt key used to start or confirm work.
* `StopButton`: Prompt key used to stop working.
* `EnterExitPassenger`, `RentBallon`, and `BallonRoutes`: Legacy compatibility variables kept for the current script structure.

### Integration Settings

```lua
SSIdentityCard = true
SSArchives = true
DecreaseFines = true
```

* `SSIdentityCard`: Intended integration with the identity office flow.
* `SSArchives`: Enables forced labor and archives integration.
* `DecreaseFines`: When `true`, withdrawn salary reduces fines first, then pays the remaining cash.

### Blip & GPS Settings

```lua
BlipStyle = "BLIP_STYLE_DEBUG_GREEN"
BlipGps = "COLOR_GREEN"
```

* `BlipStyle`: Style applied to generated job blips.
* `BlipGps`: GPS route color used for job destinations.

***

## Office Configuration

All offices and jobs are configured in:

```lua
Config.Offices
```

Each city office can contain:

* `Name`
* `Description`
* `Distance`
* `BROOM`
* `WINDOWS`
* `CARRY`

Example:

```lua
["Annesburg"] = {
    Name = "Community Jobs",
    Description = "Work & Get Paid",
    Distance = 3.0,
    ["BROOM"] = {
        Blip = -576151168,
        WorkTime = 20000,
        Pay = {0.1, 0.9},
        ForcedWork = true,
        WorkTitle = "Broom The City",
        WorkDesc = "Broom & clean the city.",
        Locations = {
            {2938.39, 1308.72, 43.57},
        },
    },
}
```

Important fields:

* `Name`: Office title shown in the jobs menu.
* `Description`: Office subtitle shown in the jobs menu.
* `Distance`: Prompt interaction range.
* `Blip`: Blip sprite hash for the job.
* `WorkTime`: Progress bar duration in milliseconds.
* `Pay`: Random salary range in `{min, max}` format.
* `ForcedWork`: If `true`, the job reduces `SS-Archives` work tasks first.
* `WorkTitle`: Menu label for the job.
* `WorkDesc`: Menu description for the job.
* `Locations`: Work destinations used by that job.
* `Start`: Used by `CARRY` as the pickup location.
* `Prop`: Used by `CARRY` as the carried object model.

***

## Job Flow

### BROOM / WINDOWS

1. The player opens the menu.
2. The player starts the selected job.
3. The script selects a random work location.
4. The player goes to the work point and presses the work prompt.
5. The progress bar completes.
6. Salary is added, or forced labor is reduced.
7. A new location is selected.

### CARRY

1. The player starts the carry job.
2. The player goes to the pickup point.
3. The player presses the work prompt and picks up the goods.
4. The script selects a random delivery point.
5. The player delivers the goods.
6. Salary is added, or forced labor is reduced.
7. The route returns to the pickup point for the next cycle.

***

## Forced Labor & Fines Logic

If integrations are enabled, the script follows this order:

1. Forced labor
2. Fines
3. Cash

This means:

* If the player still has `work > 0` in `SS-Archives`, finishing jobs reduces work tasks first.
* Once forced labor is finished, salary accumulates normally.
* When the player withdraws salary, unpaid fines are reduced first if `DecreaseFines = true`.
* Only the remaining amount is given as money.

***

## Opening The Menu From Another Script

This script exposes a client event:

```lua
TriggerEvent("SS-COMMUNITYJOBS:CLIENT:OPENJOBS", idnr, "Annesburg")
```

Arguments:

* `idnr`: Player identity number if your external flow needs it.
* City name: Must match one key from `Config.Offices`.

There is also a client export:

```lua
exports["SS-CommunityJobs"]:HasJobsInCity("Annesburg")
```

Returns:

* `true` if that city has at least one configured job.
* `false` otherwise.

***

## Notifications

All notification strings are configured in:

```text
l/l.lua
```

If you want to edit wording or add your own language, do it there.

The default notification function uses `MNotify`:

```lua
function NOTIFY(text)
    exports["MNotify"]:Notify({
        image = "maiorca.png",
        title = TR["notify_title"],
        text = text,
        duration = 5000,
        position = "center-right"
    })
end
```

***

## Add A New City

Copy an existing city block inside `Config.Offices` and change only the values:

```lua
["Valentine"] = {
    Name = "Valentine Community Jobs",
    Description = "Work for the city",
    Distance = 3.0,
    ["BROOM"] = {
        Blip = -576151168,
        WorkTime = 20000,
        Pay = {0.2, 1.0},
        ForcedWork = true,
        WorkTitle = "Clean The Streets",
        WorkDesc = "Help keep the city clean.",
        Locations = {
            {-200.0, 650.0, 113.0},
            {-180.0, 640.0, 112.8},
        },
    },
}
```

After adding a city, restart the resource/server and test the menu, prompts, blips, GPS route, payment, forced labor, and fine reduction flow.

***

## Disable A Job Type

Remove that job block from the office or leave it undefined.

Examples:

* No `WINDOWS` entry means no windows job in that city.
* No `CARRY` entry means no carry job in that city.

***

## Troubleshooting

### Menu Does Not Open

Check:

* `SS-Core`.
* Start order.
* City name passed to the open event.
* `SS-Menu` or `menuapi`, depending on your config.

### Player Cannot See Jobs In A City

Check:

* The city exists in `Config.Offices`.
* At least one of `BROOM`, `WINDOWS`, or `CARRY` exists in that office.

### Player Works But Receives No Cash

Check:

* `SSArchives = true`.
* `ForcedWork = true` in the job config.
* Whether the player still has `work` tasks in `ss_archives`.

### Salary Withdraw Gives Less Money Than Expected

Check:

* `DecreaseFines = true`.
* Whether the player still has unpaid fines in `ss_archives`.

### Menu Fails When `SSMenu = false`

Check:

* `vorp_menu`.
* `menuapi`.
* The resource providing `menuapi:getData` is started before this resource.

***

## Recommended Live Checklist

Before going live, confirm:

* Language is selected.
* Menu system is selected correctly.
* Integrations are disabled if missing.
* City names are checked.
* Job coordinates are tested.
* Salary flow works.
* Forced labor reduction works.
* Fine reduction works.

***

## Editing Rules For Beginners

When editing Lua:

* Strings use quotes: `"text"`.
* Table entries usually end with a comma: `,`.
* `true` enables a feature.
* `false` disables a feature.
* Numbers do not use quotes: `100`.
* Coordinates usually look like `{x, y, z}` or `{x, y, z, heading}`.

Bad:

```lua
SSArchives = "true"
```

Good:

```lua
SSArchives = true
```

