# Configuration

## config.lua

```lua
ServerName = 'Level Scripts',   -- notification title when a script has none

Locale = 'en',             -- language of ALL lvl scripts: 'en' or 'cs' (nil = from ox_lib)

Debug = false,             -- debug prints of all lvl scripts
```

### Bridge

```lua
-- 'auto' | 'esx' | 'qb' | 'qbx' | 'nd' | 'ox' | 'standalone'
Framework = 'auto',

-- 'auto' | 'ox_inventory' | 'qs-inventory' | 'codem-inventory' | 'core_inventory'
-- | 'tgiann-inventory' | 'origen_inventory' | 'qb-inventory' | 'ps-inventory'
-- | 'lj-inventory' | 'framework'
Inventory = 'auto',

-- 'auto' | 'ox_target' | 'qb-target' | 'none'
-- none = no target, scripts show text UI prompts instead
Target = 'auto',

-- 'auto' | 'lation_ui' | 'ox_lib'
-- switches notifications, progress bar, text UI and menus at once
UI = 'auto',

-- job money: 'auto' | 'lvl_banking' | 'okokBanking' | 'Renewed-Banking'
-- | 'qb-banking' | 'qb-management' | 'esx_addonaccount' | 'none'
Society = 'auto',
```

A single setting below wins over `UI`. For example `UI = 'lation_ui'` with `Notify.system = 'okokNotify'` uses Lation for everything except notifications.

### Notifications

```lua
Notify = {
    system = 'auto',      -- see the table above, 'custom' = your own function
    duration = 6000,      -- ms
    position = nil,       -- ox_lib only, nil = top right

    -- custom = function(data)
    --     exports.my_notify:Show(data.title, data.description, data.type, data.duration)
    -- end,
    -- data = { title, description, type ('success'|'error'|'warning'|'inform'), duration, icon }
},
```

### Progress bar

```lua
Progress = {
    system = 'auto',      -- 'none' = no bar, only the wait and the animation
    style = 'bar',        -- ox_lib only: 'bar' or 'circle'
    disable = { car = true, move = true, combat = true },
    useWhileDead = false,

    -- custom = function(data) return exports.my_progress:Start(data.label, data.duration) end,
    -- data = { label, duration, canCancel, disable, anim = { dict, clip, flag }, prop }
    -- must return true (finished) or false (cancelled)
},
```

Animation, prop, disabled controls and cancel (X) work with every progress system, also with the ones that do not support them on their own.

### Text UI and menus

```lua
TextUI = {
    system = 'auto',
    -- custom = {
    --     show = function(text, opts) exports.my_textui:Show(text) end,
    --     hide = function() exports.my_textui:Hide() end,
    -- },
},

Menu = {
    system = 'auto',      -- 'auto' = lation_ui if it is running, else ox_lib
},
```

### Units, money and jobs

```lua
Units = 'metric',     -- 'metric' (km/h, m) or 'imperial' (mph, ft)
Currency = { symbol = '$', before = true, separator = ' ' },   -- "$12 500"

PoliceJobs = { 'police', 'sheriff' },
EmergencyJobs = { 'police', 'sheriff', 'ambulance', 'lsfd', 'sahp', 'doj' },

-- groups that count as admin (ESX group, QBCore permission), ACE lvl.admin works too
AdminGroups = { admin = true, superadmin = true, owner = true, god = true },

Font = nil,           -- font name for blip labels, must be registered by another resource
ClosestPlayer = { distance = 4.0, marker = { r = 74, g = 159, b = 224, a = 160 } },
```

## server/config.lua

Only the server reads this file, players cannot download it.

```lua
-- named Discord webhooks, scripts use them by key: Config.Webhook = 'motel'
ServerConfig.Webhooks = {
    default = '',     -- used when a key is missing, empty = no log
    -- motel = 'https://discord.com/api/webhooks/...',
    -- dealership = 'https://discord.com/api/webhooks/...',
}

ServerConfig.DefaultColor = 0x2B7AC0   -- embed colour
ServerConfig.RateLimit = 25            -- max messages per webhook per minute
ServerConfig.VersionCheck = true       -- check for new versions on start
ServerConfig.JobCountCache = 10        -- seconds between job count updates
```

{% hint style="info" %}
Keep webhook URLs here, never in a `config.lua`. Players can download every `config.lua` that is a shared script.
{% endhint %}

## Commands

| Command    | Who                    | What it does                   |
| ---------- | ---------------------- | ------------------------------ |
| `/lvlcore` | server console, admins | Prints what lvl\_core detected |
