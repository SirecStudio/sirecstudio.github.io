# SS-Weapons V1.1

## Update Summary

SS-Weapons V1.1 rebuilds the whole gunsmith experience. The old book UI is replaced by a **blueprint editor** where the real weapon lies on the bench and every editable part is linked to its card with a callout line, the store becomes a **vintage catalogue**, the preview is **centred and framed automatically** for every weapon, camera and callout positions can be **tuned per weapon in game and saved as presets**, benches are **locked to one player**, **vorp\_inventory v2** is fully supported next to v1, and every purchase, edit and wear value is now **validated server-side**.

***

## Blueprint Gunsmith Editor (NEW)

* Top-down view of the real preview weapon on the bench. Every editable part (barrel, sight, scope, grip, wrap, frame, hammer, trigger, cylinder, clip, magazine, stock, blade, special finish) gets a parchment card connected to the exact spot on the weapon with a brass callout line and ring.
* Click a card to open the options drawer on the opposite side; pick components, materials, engravings, engraving metals and colours as tiles. The preview updates live, modified parts are badged and priced per change.
* Header shows weapon name, serial and live **Condition / Dirt / Rust** meters with the **Repair** button next to them.
* Footer holds camera controls (**Rotate, Zoom in, Zoom out, Reset view**), templates (save / apply / delete) and the total with **Confirm & pay** / **Cancel**.
* Cards and lines fade in only once the bench camera has finished moving.
* The weapon is unequipped while it is on the bench, so the game's weapon / ammo HUD leaves the screen; the minimap is hidden while any weapon UI is open.

***

## Vintage Catalogue Store (NEW)

* Parchment catalogue with category tabs, item list with weapon thumbnails and prices, a large engraved illustration plate, description, extra notes and stat bars per weapon.
* Custom serial and custom weapon name options with their surcharges, ammo quantity stepper with live total, "SOLD" stamp on a successful purchase.
* One atomic purchase call: the server rebuilds the price, checks money and carry space, charges and hands over the item in a single step.

***

## Auto Centering, Auto Fit & Weapon Presets (NEW)

* Weapon models pivot near the grip, so long guns used to hang off the bench. The preview is now slid so the middle of its model sits under the bench camera, and the zoom is fitted until the weapon spans a fixed share of the screen (`FitWidth` / `FitHeight`). Both run again after Rotate and Reset.
* Callout anchors are computed from the model's bounding box and bones, with fractions per weapon type in `cfg/anchors.lua`, so nothing has to be entered per weapon.
* **Per-weapon presets** (`cfg/presets.json`): with `Dev = true` the editor shows a **Weapon preset** panel to pan / turn / zoom the camera, turn the weapon on the bench and nudge every anchor. **Save preset** writes the tuning to the server file and pushes it to all clients; **Delete preset** removes it. The resource ships with presets for 32 weapons.

***

## Per-Weapon Part Lists

* A card exists only for parts the weapon really has, and shared materials / engravings only for weapon families that accept them (source: rdr3\_discoveries weapon component list). Bows, throwables and tools no longer show sight / scope / hammer cards.
* Bows can now change **frame, grip and string colour**; bladed melee weapons can change **blade material and engraving**.
* Knife grips that did not fit cleavers, hatchets and machetes were removed.

***

## vorp\_inventory v1 & v2

* Inventory version is detected from the `loadout` table (`Config.InventoryVersion` can force it) and the client runs a dedicated equip module per version: v1 draws the weapon on equip, v2 puts it in the holster, both are handled without touching the other.
* Fixed on v2: the bench used the last equipped weapon instead of the one in hand, saved components not applied after re-equip, wear stuck at 0 in `ss_weapons`, cleaning / inspection not starting. Weapons received at character select are dressed the moment they are drawn, and switching weapons through the weapon wheel is tracked.
* Item checks (cleaning item, repair kit) go through SS-Core, which now uses the version-stable inventory API.

***

## One Player Per Bench

* A bench in use is locked: another player gets "This workbench is being used by someone else" and can neither replace nor watch the current preview.
* Locks are released on Cancel, Confirm & pay and disconnect. A lock whose owner crashed, walked away from the bench (`Config.BenchLock.MaxDistance`) or sat in the editor too long (`Config.BenchLock.MaxMinutes`) is dropped automatically, and `w_freebench` in the server console frees a bench by hand.

***

## Security Hardening

* Purchases, gunsmith edits, templates and preview sessions are validated server-side: weapon ownership, distance to the counter / bench, bench job, per-weapon `ModifyJobs` / `ModifyJobsGrade`, component whitelist and prices from the server config only.
* Wear can only grow through play (`dirt`, `soot`, `degradation`, `rust` are monotonic); cleaning lowers dirt / soot / degradation and only repair lowers rust, always from the stored value, never from the client.
* Preview sessions are rebuilt from the server store config with owner checks on every update; poison / tranquilizer hits have a cooldown and a distance limit.
* Removed unused server events (`HASGOLD`, `SAVEDIRT`, `SAVEDEGRADATION`) and the two-step purchase (`HASMONEY` + `GIVEWEAPON`).

***

## Gunsmith Costs (NEW)

* Every `Config.GunSmith` price can now choose its currency: a plain number (charged in `WeaponEditPayment.Type` as before) or `{Type = "gold" | "money" | "item", Amount, Item, Label}`. A scope can require an item, its engraving gold and its material cash.
* Mixed costs are added up per currency, shown on each card, in each options group and in the total (`12 Gold · $30 · 1x Scope Lens`), and the server checks the whole amount before taking anything.
* The bench prompt text and the last hardcoded notifications are now translated in all 8 languages.

***

## Store Options

* `Serial` and `CustomLabel` per store are now honoured on client and server: `true` = paid option, `false` = hidden, `"Text"` = every weapon sold there gets that name for free.
* `ModifyJobs` / `ModifyJobsGrade` from `cfg/weapons.lua` are enforced for the bench.

***

## Fixes

* Poison effect referenced a missing config value (`DecreaseFasterStamina1`) and the tranquilizer duration was applied in milliseconds instead of seconds.
* NUI callbacks `escape`, `nothing` and `rotatewep` never answered the UI.
* Melee preview did not strip the previous material before applying a new one.
* Store `open` message ignored per-store serial / label settings.

***

## UI & Assets

* New UI is plain JavaScript (no jQuery, no turn.js), scales with screen height and looks the same on 1080p, 1440p and 4K.
* Unused fonts and the watermarked paper texture were removed; `design.js` holds the stat bars and design groups.
* New UI texts for all 8 languages (`config.js`), new notifications `no_modify_job`, `store_too_far`, `bench_busy` (`l/l.lua`).

***

## Config Changes

* New: `Config.GunsmithEditor` (zoom step, min / max FOV, callout refresh, anchor dots, `AutoCenter`, `AutoFit`, `FitWidth`, `FitHeight`), `cfg/anchors.lua`, `cfg/presets.json`, `Config.GunSmith` prices for `CYLINDER_TINT` / `BARREL_TINT` / `TRIGGER_TINT` (bow colours), `config.js` options `storeThumbs`, `calloutDots`, `calloutCurve`.
* Default stores now ship with `Serial = true` and `CustomLabel = true` to keep the previous behaviour.
* `fxmanifest.lua` lists `cfg/presets.json`; `UI/js/jsReq.js` and the unused fonts are gone.

***

## Upgrade Notes

* Replace the whole `UI/` folder, `config.js`, `cfg/anchors.lua`, `cfg/presets.json` and `l/l.lua`; merge your prices and stores into the new `config.lua`.
* On vorp\_inventory v2 keep `USE_WEAPON_DEGRADATION = false` and `USE_WEAPON_COMPONENTS = false` in the inventory config so only SS-Weapons owns wear and components.
* Set `Dev = false` on live servers; the preset panel, wear test commands and anchor diagnostics are Dev-only.
