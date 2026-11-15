---
description: >-
  Use an illegal USB, pass the hack, drive to the location, take out the armed
  guards and crack the crate for loot.
icon: usb-drive
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: hero
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# lvl\_illegalusb

[Get it on Tebex](https://level-scripts.tebex.io/package/illegalusb) | [Discord](https://www.discord.gg/UKqwhpjczw)

A short criminal mission in six difficulty colours. The player uses a USB and passes a hacking minigame. A random location appears on the GPS with a crate guarded by armed NPCs. Take them out, search the guards for the lockpick and crack the crate before the time runs out.

## Features

* **Six USB tiers** (blue, green, pink, purple, red, yellow), each with its own locations, guards and loot
* **Hacking minigame** before the mission, easy to replace
* **Armed guards** with four difficulty presets (armour, accuracy, alertness)
* **Lockpick drop**: one of the guards carries the lockpick for the crate
* **Loot table** with chance per item
* **Mission timer** on screen
* **Visibility**: guards and crate for everyone (others can join the fight) or only for the player
* **Police minimum** and **dispatch hook**
* Mission and loot are handled on the server, the crate opens only for the player who started it
* Discord log
* English and Czech, every text editable

## Requirements

| Resource                                                          |                                                        |
| ----------------------------------------------------------------- | ------------------------------------------------------ |
| [lvl\_core](../lvl_core.md)                                       | required                                               |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required                                               |
| A hacking minigame                                                | default `mhacking`, change it in `client/editable.lua` |
| A lockpick minigame                                               | default `t3_lockpick`, change it in `Config.Lockpick`  |
| Framework                                                         | any supported by lvl\_core                             |

## Installation

1. Put `lvl_illegalusb` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_illegalusb
```

3. Add the items. ox\_inventory `data/items.lua` (also in `INSTALL/ox_items.txt`):

```lua
['usb_lockpick'] = { label = 'Lockpick', weight = 160 },

['usb_blue']   = { label = 'USB Blue',   weight = 10, stack = true, close = true },
['usb_green']  = { label = 'USB Green',  weight = 10, stack = true, close = true },
['usb_pink']   = { label = 'USB Pink',   weight = 10, stack = true, close = true },
['usb_purple'] = { label = 'USB Purple', weight = 10, stack = true, close = true },
['usb_red']    = { label = 'USB Red',    weight = 10, stack = true, close = true },
['usb_yellow'] = { label = 'USB Yellow', weight = 10, stack = true, close = true },
```

A QBCore version is in `INSTALL/qb_items.txt`.

4. Connect your hacking minigame (`client/editable.lua`), lockpick minigame and dispatch (`config.lua`).
5. Put the USBs into your shops, loot tables or crafting.

## How it works

1. Use a USB item. The hacking minigame starts. A failed hack keeps the USB.
2. A location shows on the GPS. The mission timer starts.
3. Take out the guards. Search them (target or E) until you find the lockpick.
4. Open the crate with the lockpick minigame and get the loot.

If the time runs out, the mission ends.

## Configuration

### General

```lua
Config.Debug = false

Config.Interact = 'target'      -- 'target' or 'textui'
Config.PressKey = 38            -- E, for textui
Config.Webhook = ''             -- Discord webhook, '' = off

Config.ShowMissionTimer = true
Config.MissionTime = 300        -- seconds

-- 'all' = everyone sees guards and crate, 'player' = only the player who started it
Config.MissionVisibility = 'all'

Config.MinPolice = 0            -- police online needed
```

### Guard difficulty

```lua
Config.GuardDifficulties = {
    easy     = { armour = 0,   alertness = 1, accuracy = 40, range = 0, ability = 0 },
    medium   = { armour = 0,   alertness = 2, accuracy = 60, range = 2, ability = 1 },
    hard     = { armour = 50,  alertness = 3, accuracy = 80, range = 2, ability = 2 },
    veryhard = { armour = 100, alertness = 3, accuracy = 95, range = 2, ability = 2 },
}
```

### USBs

The key is the item name.

```lua
Config.Usbs = {
    usb_blue = {
        prop = 'm23_1_prop_m31_crate_cd_01a',   -- crate
        locations = {                           -- one is picked at random
            vec3(-576.94, 325.88, 84.69),
            vec3(-693.94, -981.01, 20.38),
            vec3(799.70, -1611.37, 31.28),
        },
        guardCount = 4,
        guardPed = "s_m_y_blackops_01",
        guardDifficulty = "easy",               -- key from Config.GuardDifficulties
        guardWeapon = "WEAPON_PISTOL",
        loot = {
            { item = 'black_money', count = 4000, chance = 100 },
            { item = 'ammo-9', count = 100, chance = 50 },
            { item = 'weapon_pistol', count = 1, chance = 10 },
        },
    },
    -- usb_green, usb_pink, usb_purple, usb_red, usb_yellow
}
```

Add a new tier by adding an entry here and an item with the same name.

### Minigames

Hacking, `client/editable.lua`:

```lua
function StartHack(itemName)
    TriggerEvent('mhacking:show')
    TriggerEvent('mhacking:start', 7, 35, function(success)
        TriggerEvent('mhacking:hide')
        HackResult(success)   -- call with true or false
    end)
end
```

Lockpick, `config.lua`:

```lua
Config.LockpickItem = "usb_lockpick"
Config.Lockpick = function()
    return exports["t3_lockpick"]:startLockpick(Config.LockpickItem, 1, 1)   -- must return true or false
end
```

### Dispatch

Called on the client when the player gets close to the location. Default is cd\_dispatch, replace it with your dispatch:

```lua
Config.Dispatch = function()
    -- your dispatch export or event here
end
```

## Items

| Item                                                                       | Use                                 |
| -------------------------------------------------------------------------- | ----------------------------------- |
| `usb_blue`, `usb_green`, `usb_pink`, `usb_purple`, `usb_red`, `usb_yellow` | Start a mission of that tier        |
| `usb_lockpick`                                                             | Dropped by a guard, opens the crate |

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>Using the USB does nothing</summary>

Check the police minimum (`Config.MinPolice`) and that the hacking minigame resource is running. Without it the hack never ends. Replace `StartHack` in `client/editable.lua` with your minigame.

</details>

<details>

<summary>Part of the loot is missing</summary>

The inventory was full. The player gets a notification, the rest of the loot is lost.

</details>
