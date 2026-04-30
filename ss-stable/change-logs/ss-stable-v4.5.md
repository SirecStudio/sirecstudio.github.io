# SS-Stable V4.5

## Update Summary

This update focuses on horse spawning, training, horseshoes, foal visuals, equipment behavior, inventory quality-of-life improvements, and new configuration options for horse drinking props and inventory limits.

***

## Fixes & Improvements

* Fixed an issue where calling a horse could sometimes duplicate the horse or trigger an F8 error.
* Fixed route-based training experience not being saved correctly.
* Fixed an issue that allowed players to equip more than 4 horseshoes on one horse.
* Fixed mount behavior for foals after new skins were added, ensuring foals correctly receive the new skin data.
* Fixed horse statistics when horses were created or loaded with different stat values.
* Fixed extra equipment removal when the buttons were not activating correctly.
* Improved inventory behavior while carrying an entity. Inventory buttons no longer appear during this action, making it easier to place players, animals, or skins on a horse.
* Fixed horse mane and tail visuals so modified values are visible correctly on the horse.
* Fixed stable and equipment preview behavior so horses with custom skins display correctly instead of showing the default horse.

***

## Added

* Added support for custom water props when horses drink water.
* Added a horse inventory limit option through `IgnoreItemsLimit`.
* Added improved horse tricks behavior. The `horsetricks` function can now work through a command, or through horse petting when the command is disabled in config.

***

## Config

### Drinking Props

You can now define which props are valid for horse drinking interactions:

```lua
DrinkingProps = {
    "p_watertrough02x",
    "p_watertrough01x",
    "p_watertrough03x",
    "p_watertrough01x_new",
    "p_watertroughsml01x",
}
```

### Horse Inventory Limit

Horse inventory behavior can now be controlled from config:

```lua
IgnoreItemsLimit = false
```

* `true`: Horse inventory ignores the normal item limit.
* `false`: Horse inventory follows the same item limit behavior as the player inventory.

### Horse Tricks Command

Horse tricks can be configured to use a command or a petting interaction:

```lua
HorseTricksCommand = false
```

* Set a command name to enable command-based horse tricks.
* Set to `false` to disable the command and use the configured interaction behavior instead.
