# Configuration

## General

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

## Guard difficulty

```lua
Config.GuardDifficulties = {
    easy     = { armour = 0,   alertness = 1, accuracy = 40, range = 0, ability = 0 },
    medium   = { armour = 0,   alertness = 2, accuracy = 60, range = 2, ability = 1 },
    hard     = { armour = 50,  alertness = 3, accuracy = 80, range = 2, ability = 2 },
    veryhard = { armour = 100, alertness = 3, accuracy = 95, range = 2, ability = 2 },
}
```

## USBs

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

## Minigames

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

## Dispatch

Called on the client when the player gets close to the location. Default is cd\_dispatch, replace it with your dispatch:

```lua
Config.Dispatch = function()
    -- your dispatch export or event here
end
```
