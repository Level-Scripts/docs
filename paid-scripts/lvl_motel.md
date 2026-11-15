---
description: >-
  Motel rooms with rent, shared keys with permissions, private stash, wardrobe,
  room tours and police raids.
icon: hotel
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

# lvl\_motel

[Buy on Tebex](https://level-scripts.tebex.io/package/motel) | [Discord](https://www.discord.gg/UKqwhpjczw)

Players rent a motel room at its door, pay for days in advance and get a private room with a stash and a wardrobe. The tenant can share the key with friends and choose what each of them may do. Police can seal a room, open its stash and breach a locked door. Every room is its own instance, so many players can use the same interior at once.

## Features

* **Rent at the door**: pick the days, pay with cash or bank
* **Room tour** before renting
* **Rent expiry**: the room is released when the rent runs out, with a warning on join, and the stash is emptied for the next tenant
* **Extend rent** up to a max of prepaid days
* **Shared keys** with permissions: storage, wardrobe, give access, extend rent
* **Private stash** and **wardrobe** inside the room
* **Lock and unlock** the door
* **Police**: seal and unseal a room, breach a locked door with a ram item
* **Society share**: part of every rent goes to a job account
* **Instanced rooms** (routing buckets), players who disconnect inside are moved to the door
* **Server side checks** for price, distance and permissions
* **Discord logs** for rent, keys and police actions
* English and Czech, every text editable

## Requirements

| Resource                                                                      |                            |
| ----------------------------------------------------------------------------- | -------------------------- |
| [lvl\_core](../lvl_core.md)                                                   | required                   |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)             | required                   |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest)            | required                   |
| [ox\_inventory](https://github.com/overextended/ox_inventory/releases/latest) | required (stash)           |
| ESX, QBCore or Qbox                                                           | detected automatically     |
| illenium-appearance, qb-clothing or esx\_skin                                 | optional, for the wardrobe |

## Installation

1. Put `lvl_motel` into your resources.
2. Add it to `server.cfg` after ox\_inventory and lvl\_core:

```
ensure ox_inventory
ensure lvl_core
ensure lvl_motel
```

3. Add the police item to `ox_inventory/data/items.lua` (also in `INSTALL/ox_item.txt`):

```lua
['police_ram'] = {
    label = 'Police ram',
    weight = 8000,
    stack = false,
},
```

4. Copy `INSTALL/police_ram.png` to `ox_inventory/web/images/`.
5. Give the `police_ram` to your police (armory, shop or job items).
6. Set motels, prices and room doors in `config/config.lua`.
7. Start the server. Tables are created automatically. Rooms from the old `motel` tables are copied once.

## How it works

| Who                    | At the door                                             |
| ---------------------- | ------------------------------------------------------- |
| Anyone                 | Rent a free room, take a tour                           |
| Tenant and key holders | Enter, lock, unlock, extend rent, manage the room       |
| Police                 | Open police actions: seal, remove seal, breach the door |

Inside the room are the stash and the wardrobe. A key holder only sees what the tenant allowed. A key holder can only give permissions they have themselves.

## Configuration

### General

```lua
Config.Framework = 'auto'   -- 'auto' | 'esx' | 'qb' | 'qbx'
Config.Webhook = 'motel'    -- key in lvl_core/server/config.lua or a full webhook URL

Config.Interact = 'textui'  -- 'textui' (key at the door) or 'ox_target'
Config.PressKey = 38        -- E, for textui
Config.DoorDistance = 6.0   -- max distance from the door for any action (checked by the server)

Config.TimeForPreview = 30  -- room tour length in seconds

Config.Blip = { enabled = false, sprite = 475, color = 3, scale = 0.7 }   -- map blip per motel
```

### Police

```lua
Config.PoliceJobs = { 'police', 'sheriff' }
Config.PoliceOnDuty = true          -- QBCore and Qbox: only on duty officers
Config.ItemForOpen = 'police_ram'   -- item needed to breach a door
Config.RaidTime = 5000              -- ms
```

### Rent

```lua
Config.Society = { enabled = true, job = 'police', percent = 50 }   -- part of every rent to a job account

Config.Limit = 2                 -- rooms one player can rent in one motel
Config.RentDays = { 7, 14 }      -- rent options in days
Config.MaxDays = 60              -- max days paid in advance

Config.RentExpires = true        -- release the room when the rent runs out
Config.ClearStashOnExpiry = true -- empty the stash for the next tenant
Config.WarnDays = 1              -- warn on join when this many days are left
Config.ExpiryCheckMinutes = 30
```

### Wardrobe

```lua
Config.OutfitMenu = function()
    if GetResourceState('illenium-appearance') == 'started' then
        TriggerEvent('illenium-appearance:client:openOutfitMenu')
    elseif GetResourceState('qb-clothing') == 'started' then
        TriggerEvent('qb-clothing:client:openOutfitMenu')
    elseif GetResourceState('esx_skin') == 'started' then
        TriggerEvent('esx_skin:openSaveableMenu')
    end
end
```

Replace it with the outfit menu of your clothing script.

### Routing buckets

```lua
Config.Buckets = { room = 50000, preview = 60000 }
```

Room instance = `room + room id`, tour = `preview + player id`. Change them only if another script uses the same numbers.

### Motels and rooms

```lua
Config.Motel = {
    ["Perrera Beach"] = {
        label = "Perrera Beach",
        price = 500,                 -- per day
        image = 'https://...',       -- picture in the rent window
        point = {
            [1] = { roomNumber = 1, pos = vector3(-1493.75, -668.36, 29.02), interior = "motel_small" },
            [2] = { roomNumber = 2, pos = vector3(-1498.18, -664.70, 29.02), interior = "motel_small" },
            -- one line per door
        },
    },
}
```

* `pos` is the position of the room door outside.
* `interior` is a key from `config/ipl.lua`.

Included motels: **Perrera Beach** and **The Pink Cage** with all room doors set. **Bilingsgate**, **The Motor**, **Eastern** and **Dream View** are prepared without rooms, add their doors the same way.

### Interiors

`config/ipl.lua`:

```lua
IPL = {
    list = {
        ["motel_small"] = {
            label = "motel_small",
            weight = 100000,   -- stash max weight (grams)
            slots = 100,       -- stash slots
            EntrancePos = { x = 151.40, y = -1007.87, z = -99.00 },
            storagepos = { x = 151.31, y = -1003.12, z = -99.00 },
            cloakroompos = { x = 151.77, y = -1001.32, z = -99.00 },
        },
    }
}
```

Add more interiors here and use their key in `interior` of a room.

## Items

| Item         | Use                                                            |
| ------------ | -------------------------------------------------------------- |
| `police_ram` | Police breach a locked door. Name set in `Config.ItemForOpen`. |

## Database

Created automatically. `INSTALL/lvl_motel.sql` only if your database user cannot create tables.

| Table              | Content                                       |
| ------------------ | --------------------------------------------- |
| `lvl_motel_rooms`  | Rented rooms, tenant, rent end, lock and seal |
| `lvl_motel_keys`   | Key holders and their permissions             |
| `lvl_motel_inside` | Players who were inside a room when they left |

The old tables `motel`, `motel_key` and `motel_inside` from v1 are copied once and can be deleted after that.

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>The rent money goes to the police</summary>

That is the default share in `Config.Society`. Set another job, another percent, or `enabled = false`.

</details>

<details>

<summary>The wardrobe does nothing</summary>

`Config.OutfitMenu` supports illenium-appearance, qb-clothing and esx\_skin. For another clothing script put its outfit menu event or export there.

</details>

<details>

<summary>How do I add a motel?</summary>

Add a new entry to `Config.Motel` with a label, price, image and one `point` per door. Stand at the door in game, copy your coordinates and use them as `pos`.

</details>
