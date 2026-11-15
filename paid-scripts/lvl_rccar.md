---
description: >-
  Remote controlled cars with a camera, microphone, antenna and swappable
  batteries. Every car is an item that keeps its name, parts and charge.
icon: gamepad-modern
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

# lvl\_rccar

[Buy on Tebex](https://level-scripts.tebex.io/package/rccar) | [Discord](https://www.discord.gg/UKqwhpjczw)

Players place an RC car from their inventory and drive it with a controller. Install a camera to drive from the car view (normal, night vision, thermal), a microphone to hear what is around it and an antenna for a longer signal. The battery drains while driving and can be swapped. Each car item remembers its own name, parts and battery, so it can be traded or sold.

## Features

* **Place and drive** RC cars with a controller item
* **Car view camera** with normal, night vision and thermal modes
* **Microphone** to hear the surroundings of the car
* **Antenna** for a longer signal range
* **Battery** that drains by distance, battery items keep their charge, swapping returns the old battery
* **Rename** every car
* **HUD** with distance, battery and signal
* **Car is an item** with its own data, cars left out on disconnect or restart return to the inventory
* **Job lock** per car model (for example a police RC car)
* **Shop** with ox\_inventory, blip and target
* **Server side** checks for every action
* English and Czech, every text editable

## Requirements

| Resource                                                                      |                        |
| ----------------------------------------------------------------------------- | ---------------------- |
| [lvl\_core](../lvl_core.md)                                                   | required               |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)             | required               |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest)            | required               |
| [ox\_inventory](https://github.com/overextended/ox_inventory/releases/latest) | required               |
| ox\_target or qb-target                                                       | required               |
| ESX, QBCore or Qbox                                                           | detected automatically |

## Installation

1. Put `lvl_rccar` into your resources.
2. Add it to `server.cfg` after ox\_inventory and lvl\_core:

```
ensure ox_inventory
ensure lvl_core
ensure lvl_rccar
```

3. Add the items to `ox_inventory/data/items.lua` (also in `INSTALL/ox_items.txt`):

```lua
['rcbandito'] = {
    label = 'RC Bandito',
    weight = 1500,
    stack = false,
    close = true,
    description = 'Remote controlled car',
    client = { export = 'lvl_rccar.placeRCcar' },
},

['controller'] = {
    label = 'RC Controller',
    weight = 300,
    stack = false,
    close = true,
    description = 'Drive your placed RC cars',
    client = { export = 'lvl_rccar.useController' },
},

['rc_camera'] = { label = 'RC Camera', weight = 100, stack = true, close = true },
['rc_microphone'] = { label = 'RC Microphone', weight = 50, stack = true, close = true },
['rc_antenna'] = { label = 'RC Antenna', weight = 80, stack = true, close = true },
['rc_battery'] = { label = 'RC Battery', weight = 200, stack = false, close = true },
```

4. Put an image for every item into `ox_inventory/web/images/` named after the item (`rcbandito.png`, `controller.png`...).
5. Restart. The table is created automatically, cars from the old `rc_cars` table are copied once.

## How to use

1. Use the **RC car** item to place it on the ground.
2. Target the car: **Pick up** or **Car options** (rename, battery, camera, microphone, antenna).
3. Use the **controller** item, pick a car from the list and drive.

### Controls

| Key    | Action           |
| ------ | ---------------- |
| Arrows | Drive and steer  |
| `G`    | Camera on or off |
| `H`    | Next camera mode |
| `E`    | Disconnect       |

Leaving the signal range or an empty battery disconnects you.

## Configuration

`config.lua`:

```lua
Config.Framework = 'auto'   -- 'auto' | 'esx' | 'qb' | 'qbx'

-- ox_inventory item names
Config.Items = {
    controller = 'controller',
    camera     = 'rc_camera',
    microphone = 'rc_microphone',
    antenna    = 'rc_antenna',
    battery    = 'rc_battery',
}

Config.Range = 100.0             -- signal range in metres
Config.AntennaBonus = 50.0       -- metres added by the antenna
Config.BatteryDistance = 1000.0  -- metres a full battery lasts
Config.MaxPlaced = 2             -- cars one player can have placed at once
Config.DefaultName = 'RC Car #%d'
```

### Cars

The key is the item name of the car.

```lua
Config.Cars = {
    rcbandito = {
        model = 'rcbandito',
        job = nil,              -- nil = everyone, 'police' or { 'police', 'sheriff' }
        camera = {
            enabled = true,
            normal = true,
            nightVision = true,
            thermal = true,
        },
    },
}
```

To add another RC car, add an entry here and an item with the same name and `client = { export = 'lvl_rccar.placeRCcar' }`.

### Shop

```lua
Config.Shop = {
    name = 'RC Shop',
    inventory = {
        { name = 'rcbandito', price = 2000 },
        { name = 'controller', price = 500 },
        { name = 'rc_camera', price = 1000 },
        { name = 'rc_microphone', price = 700 },
        { name = 'rc_antenna', price = 600 },
        { name = 'rc_battery', price = 300 },
    },
    locations = {
        vec3(-1524.21, -409.38, 34.59),
    },
    blip = { sprite = 646, colour = 3, scale = 0.7 },   -- false = no blip
}
```

Set `Config.Shop = false` to sell the items in another shop.

## Items

| Item            | Use                                                       |
| --------------- | --------------------------------------------------------- |
| `rcbandito`     | The RC car, keeps its name, parts and battery in the item |
| `controller`    | Opens the list of your placed cars                        |
| `rc_camera`     | Installs the camera                                       |
| `rc_microphone` | Installs the microphone                                   |
| `rc_antenna`    | Installs the antenna                                      |
| `rc_battery`    | Swaps the battery, keeps its own charge                   |

## Exports

Client exports used by the items:

| Export                                     |                                      |
| ------------------------------------------ | ------------------------------------ |
| `exports.lvl_rccar:placeRCcar(data, slot)` | Places the RC car from the used item |
| `exports.lvl_rccar:useController()`        | Opens the controller                 |

## Database

Created automatically. `INSTALL/lvl_rccar.sql` only if your database user cannot create tables.

| Table            | Content                                                         |
| ---------------- | --------------------------------------------------------------- |
| `lvl_rccar_cars` | Every RC car: owner, name, model, parts, battery, placed or not |

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>No such export RegisterShop in resource ox_inventory</summary>

ox\_inventory had an error on start, so its shop export was never created. Fix the first ox\_inventory error in the console. lvl\_rccar retries for 30 seconds and registers the shop again when ox\_inventory restarts.

</details>

<details>

<summary>Using the item does nothing</summary>

The item needs `client = { export = 'lvl_rccar.placeRCcar' }` (car) or `client = { export = 'lvl_rccar.useController' }` (controller) in `items.lua`.

</details>
