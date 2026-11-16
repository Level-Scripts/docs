# Configuration

Framework, inventory and target are set in [lvl\_core configuration](../../lvl_core/configuration.md).

## General

```lua
Config.Webhook = 'motel'    -- key in lvl_core/server/config.lua or a full webhook URL

Config.Interact = 'textui'  -- 'textui' (key at the door) or 'ox_target'
Config.PressKey = 38        -- E, for textui
Config.DoorDistance = 6.0   -- max distance from the door for any action (checked by the server)

Config.TimeForPreview = 30  -- room tour length in seconds

Config.Blip = { enabled = false, sprite = 475, color = 3, scale = 0.7 }   -- map blip per motel
```

## Police

```lua
Config.PoliceJobs = { 'police', 'sheriff' }
Config.PoliceOnDuty = true          -- QBCore and Qbox: only on duty officers
Config.ItemForOpen = 'police_ram'   -- item needed to breach a door
Config.RaidTime = 5000              -- ms
```

## Rent

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

## Wardrobe

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

## Routing buckets

```lua
Config.Buckets = { room = 50000, preview = 60000 }
```

Room instance = `room + room id`, tour = `preview + player id`. Change them only if another script uses the same numbers.

## Motels and rooms

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

## Interiors

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
