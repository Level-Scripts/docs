# Configuration

All options are in `config.lua`. Secrets are in `server/config.lua`.

## General

```lua
Config.Debug = false

Config.Framework = 'auto'      -- 'auto' | 'esx' | 'qb' | 'qbx'
Config.Interact = 'auto'       -- 'auto' | 'ox_target' | 'qb-target' | 'textui'
Config.InteractKey = 38        -- E, only for textui

-- company money: 'auto' | 'esx_addonaccount' | 'qb-banking' | 'qb-management' | 'renewed-banking' | 'none'
Config.Society = 'auto'

Config.AdminCommand = 'dealeradmin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }

Config.AutoCreateJobs = true   -- create dealership jobs, grades and company accounts on start
Config.Blips = true            -- map blip for every dealership

Config.PlateFormat = 'NLLL NNN'   -- L = letter, N = number, other characters are kept, max 8
```

## Company vehicles

```lua
Config.JobVehicleColumn = nil      -- column in your vehicles table for the job, e.g. 'job'
Config.JobGradeColumn = nil        -- column for the min. grade, e.g. 'grade'
Config.CompanyBuyGrades = { 'boss' }   -- grades that may buy cars for the job
```

Without `JobVehicleColumn` a car bought for the company is saved as a normal owned car.

## Financing

```lua
Config.Financing = {
    enabled = true,
    payments = 10,        -- equal payments of price + interest, the first one is paid at purchase
    interval = 1,         -- hours between payments
    interest = 8,         -- % on top of the price
    maxActive = 2,        -- financed vehicles per player
    repossessAfter = 3,   -- missed payments before the car is taken back (0 = never)
    payoff = true,        -- "Pay off" button: pay the rest at once
}
```

A financed car cannot be sold back or returned until it is paid off.

## Colours

```lua
Config.Colors = {
    mode = 'rgb',     -- 'rgb' | 'palette' | 'gta' | false (no colour step)
    palette = { { label = 'White', hex = '#F2F2F2' }, ... },
    gta = { { id = 0, label = 'Metallic Black', hex = '#0D1116' }, ... },
}
```

| Mode | Result |
| --- | --- |
| `rgb` | Full colour picker |
| `palette` | Only your colours from `palette` |
| `gta` | GTA paints from `gta` (`id` = paint index, `hex` = swatch colour in the tablet) |
| `false` | No colour step, the car keeps its default colour |

## Extras

```lua
Config.Creator = { enabled = true }    -- Settings page in /dealeradmin

Config.Currency = {                    -- dealerships with currency = true sell only for this
    enabled = false,
    label = 'Coins',
}

Config.Stats = { enabled = true, days = { 7, 30, 90 } }   -- statistics in the boss tablet

Config.Compare = true                  -- compare two cars in the catalog

Config.CustomPlate = {
    enabled = true,
    price = 5000,
    min = 2,
    max = 8,
    blocked = { 'FUCK', 'POLICE', 'ADMIN', ... },   -- also catches 0/1/3/4/5/7 look-alikes and spaces
}

Config.ReturnHours = 2                 -- return a new car for a full refund (0 = off)
Config.DiscountItem = 'discount_code'  -- voucher item, the code is in its metadata
Config.CheckSpawnPoint = true          -- do not spawn a bought car on a blocked spot
Config.ShowroomDistance = 90.0         -- showroom cars exist only this close
```

## Test drive

```lua
Config.TestDrive = {
    duration = 90,          -- seconds
    endKey = 47,            -- G
    plate = 'TEST',
    privateWorld = true,    -- own routing bucket, nobody gets in the way
    damageFee = 500,        -- max fee for a wrecked car, scaled by damage
}
```

## Stock orders

Only for `owned` dealerships. A car can be ordered when it has a stock number in the catalog (empty stock = unlimited, no ordering).

```lua
Config.Orders = {
    deliveryFee = 2500,        -- per truck, paid from the company account
    deliveryDelay = 60,        -- seconds until the trucks set off
    pickupDelay = 60,          -- seconds until the order waits at the depot
    waitMinutes = 10,          -- trucks leave when nobody signs
    stuckSeconds = 20,         -- a truck standing on a free road this long gets a new route
    approach = 18.0,           -- metres before the unload spot where the truck lines up
    hostDistance = 250.0,      -- delivery starts only when a staff member is this close
    truck = 'hauler',
    trailer = 'tr2',
    driver = 's_m_m_trucker_01',
    blips = { route = {...}, truck = {...} },
    slots = { vec4(0.0, 5.6, 2.85, 0.0), ... },   -- car positions on the trailer = truck capacity
    depot = {
        label = 'Port of Los Santos',
        clerk = { model = 's_m_y_dockwork_01', coords = vec4(...) },
        parking = { vec4(...), ... },
    },
}
```

* **Delivery**: trucks drive from the dealership `delivery.from` point to `delivery.unload`, obey traffic lights and park. A staff member signs at the driver and the cars go to stock.
* **Pickup**: the boss gets a GPS route to the depot, signs at the clerk and drives the loaded trucks to the dealership one by one.

Set `delivery.from` and `delivery.unload` for each dealership on its Settings page. Without them only Pickup works. Preview the trailer slots in `/dealeradmin`, Tools, Trailer preview.

## Discord logs

```lua
Config.Webhooks = {
    enabled = true,
    buy = true, sell = true, order = true, intake = true, finance = true,
    money = true, staff = true, catalog = true, creator = true,
}
```

Where a log goes, first match wins:

1. Webhook of the dealership and event (set in `/dealeradmin`, Webhooks)
2. Webhook of the dealership for all events
3. `ServerConfig.Webhooks[event]` in `server/config.lua`
4. `ServerConfig.Webhook` in `server/config.lua`

## server/config.lua

```lua
-- a full Discord URL or a key from lvl_core/server/config.lua
ServerConfig.Webhook = 'dealership'

ServerConfig.Webhooks = { buy = '', sell = '', order = '', ... }

-- custom currency, connect your coin system
ServerConfig.Currency = {
    balance = function(src) return exports.my_coins:GetCoins(src) end,
    remove = function(src, amount) return exports.my_coins:RemoveCoins(src, amount) end,
    add = function(src, amount) return exports.my_coins:AddCoins(src, amount) end,
}
```

## Hooks

Client functions in `config.lua` for your keys and fuel scripts:

```lua
Config.OnVehicleSpawned = function(vehicle, plate, model)
    -- exports.my_keys:GiveKeys(plate)
    -- exports['cdn-fuel']:SetFuel(vehicle, 100.0)
    Entity(vehicle).state.fuel = 100.0
end

Config.OnTestDriveStart = function(vehicle, plate, model) end
Config.OnTestDriveEnd = function(vehicle, plate, model) end
```
