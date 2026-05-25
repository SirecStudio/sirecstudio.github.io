# SS-Telegram V4.5

## Update Summary

SS-Telegram V4.5 is a major feature and stability update focused on the telegram sending experience, location sharing, configurable money/location options, automatic database setup, and better UI behavior.

This update also improves the bird delivery flow and adds stronger server-side validation so disabled features cannot be forced through NUI or client-side data.

***

## Added

* Added location sharing for normal telegrams.
* Added temporary map blip and GPS route support when a telegram contains shared coordinates.
* Added saved coordinate support for old telegram items, allowing location telegrams to be viewed again later.
* Added `EnableSendMoney` config option to fully enable or disable money attachments.
* Added `EnableShareLocation` config option to fully enable or disable location sharing.
* Added `AutoSetupDatabase` config option for automatic table and column setup.
* Added receiver name autocomplete/ghost preview inside the telegram UI.
* Added database repair checks for missing required columns.

***

## Location Sharing

Players can now attach their current location to a normal telegram.

When location sharing is enabled:

* the sender can select the location option from the telegram UI
* the script stores the sender coordinates in the `coords` database column
* the receiver sees the sent location zone on the telegram
* a temporary map blip is created for the shared position
* a GPS route points the receiver to the shared location
* old saved telegram items can show the shared location again when read later

When `EnableShareLocation = false`:

* the location option is hidden from the UI
* the client `getcoords` callback returns `false`
* new telegrams do not save coordinates
* old saved coordinates are ignored
* no blip or GPS route is created when receiving or reading telegrams

***

## Config & Database

Added new configuration controls in `config.lua`:

```lua
AutoSetupDatabase = true
EnableSendMoney = true
EnableShareLocation = true
```

`AutoSetupDatabase` prepares the required SQL structure on resource start.

The setup process now supports:

* `CREATE TABLE IF NOT EXISTS` for `ss_telegram`
* `CREATE TABLE IF NOT EXISTS` for `ss_telegramlist`
* `SHOW COLUMNS` checks for required fields
* `ALTER TABLE ADD COLUMN` only when a column is missing
* automatic checks for fields such as `money`, `coords`, `isread`, `destid`, sender data, and recipient data

The MySQL database/schema itself must still exist in the `oxmysql` or `ghmattimysql` connection string before the resource starts.

***

## UI Improvements

* Improved the send telegram UI flow.
* Added receiver autocomplete with a ghost text preview for faster name entry.
* Updated the UI to hide money and location options when the related config option is disabled.
* Updated location selection so the selected zone name is displayed after coordinates are captured.
* Improved read telegram metadata so shared locations can show a clear `Sent from` label.
* Preserved anonymous telegram behavior by keeping money and location options hidden for anonymous sends.

***

## Animations & Interaction

* Added improved telegram inspection animations for live telegram writing and reading.
* Added separate old telegram item interaction flow when reading saved telegrams from inventory.
* Improved enter/exit animation handling when opening or closing the telegram UI.
* Improved the player interaction flow around calling, writing, reading, and closing telegrams.

***

## Money & Security

Money sending can now be disabled completely with:

```lua
EnableSendMoney = false
```

When disabled:

* the money option is hidden from the UI
* client/NUI money values are forced to `0`
* the server ignores manually sent money values
* receivers do not receive money from disabled money telegrams

The server also keeps validation for maximum money amount, whole number checks, and sender balance checks.

***

## Bird Delivery Flow

* Improved the bird delivery logic around the player.
* Improved bird landing and hover behavior during read/send flows.
* Improved failsafe handling for stuck or invalid bird states.
* Reduced cases where birds could get stuck around buildings or bad landing positions.

***

## Stability & Performance

* Added stronger config-based validation on both client and server.
* Improved old telegram reading so disabled location sharing does not create legacy blips.
* Improved compatibility for older telegrams that stored coordinates before the dedicated `coords` column.
* Improved database compatibility with both `oxmysql` and `ghmattimysql`.
* Updated README documentation for the new configuration options, location sharing flow, automatic database setup, and troubleshooting notes.
