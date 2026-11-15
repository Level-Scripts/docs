---
description: >-
  Car, boat and air dealerships with showroom, test drives, financing, used car
  lot, company management, stock delivery trucks and an in-game admin panel.
icon: car
cover: ../.gitbook/assets/nahledak dealership.png
coverY: -348
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

# lvl\_dealership

[Buy on Tebex](https://level-scripts.tebex.io/package/dealership) | [Discord](https://www.discord.gg/UKqwhpjczw)

A complete dealership system. Players browse the catalog on a tablet, test drive, pick a colour and a plate and pay at once or in installments. Owned dealerships are run by players: employees, company money, stock orders delivered by NPC trucks and sales statistics. Admins create and edit every dealership in game, no restart needed.

## Features

* **Three dealership types**: self-service shop, player owned company and used car lot (bazaar)
* **Catalog tablet** with categories, search, vehicle specs and side by side compare
* **Showroom** cars placed in game by the staff, spawned only near the dealership
* **Test drives** with a timer, in a private world, with a damage fee
* **Colour step**: full RGB picker, your own palette or GTA paints (metallic, matte, chrome)
* **Custom plate** for a fee, with a blocked word list
* **Financing**: equal payments with interest, automatic charges, repossession after missed payments, early payoff
* **Discount codes** and voucher items with the code inside
* **Return window**: return a new car for a full refund within a set time
* **Sell back** to the dealership for a percentage of the price
* **Company management** tablet for bosses: staff, grades, company account, deposits and withdrawals (bank or cash), transactions, statistics
* **Stock orders**: the boss fills a cart, NPC trucks with car trailers drive to the dealership, staff signs at the driver; or pick the trucks up at the port yourself
* **Used car lot**: employees buy cars from players and resell them with the same plate and tuning
* **Company vehicles**: bosses buy cars for their job
* **Custom currency**: a dealership can sell only for coins or tokens
* **Admin panel** `/dealeradmin`: dealerships, catalog, orders, loans, sales log, discount codes, webhooks, tools
* **Discord logs** per dealership and per event
* Jobs and company accounts are created automatically
* English and Czech, every text editable

## Requirements

| Resource                                                           |                                            |
| ------------------------------------------------------------------ | ------------------------------------------ |
| [lvl\_core](../lvl_core.md)                                        | required                                   |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)  | required                                   |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest) | required                                   |
| ESX, QBCore or Qbox                                                | detected automatically                     |
| ox\_target or qb-target                                            | optional, text UI prompts without it       |
| ox\_inventory                                                      | optional, for trunk info and voucher items |

## Installation

1. Put `lvl_dealership` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_dealership
```

3. Start the server. All tables are created automatically. On the first start the starter dealerships from `server/starter.lua` are copied into the database once.
4. Join the game and open `/dealeradmin` to check the dealerships and add vehicles to the catalog.
5. Optional, for discount vouchers, add the item to `ox_inventory/data/items.lua`:

```lua
['discount_code'] = {
    label = 'Discount voucher',
    weight = 10,
    stack = false,
},
```

6. Connect your car keys and fuel in `Config.OnVehicleSpawned` (see [Hooks](lvl_dealership.md#hooks)).

{% hint style="info" %}
Coming from v1? Data from the old tables (vehicles, categories, showroom, codes, settings) is copied on the first start. Nothing is deleted.
{% endhint %}

## Starter dealerships

| ID | Name                      | Type                                   | Vehicles  |
| -- | ------------------------- | -------------------------------------- | --------- |
| 1  | Premium Deluxe Motorsport | Owned, job `pdm`, stock delivery       | cars      |
| 2  | Boat Shop                 | Self-service, needs license `boat`     | boats     |
| 3  | Air Shop                  | Self-service, needs license `aircraft` | aircraft  |
| 4  | Bike Shop                 | Self-service                           | bikes     |
| 5  | Car Bazaar                | Used car lot, job `carbazaar`          | used cars |

After the first start `server/starter.lua` is not used anymore. Create, edit and delete dealerships in `/dealeradmin`. To start over from the starter list, delete all rows of `lvl_dealership_locations` and restart.

## Dealership types

| Type           | How it works                                                                                                     |
| -------------- | ---------------------------------------------------------------------------------------------------------------- |
| `self-service` | A shop without employees. Players buy directly from the catalog. Stock is optional.                              |
| `owned`        | A company with a job. Employees sell, the boss manages money, staff and stock. Sales go to the company account.  |
| `bazaar`       | Used car lot. Employees buy cars from players in the intake zone, then sell them with the same plate and tuning. |

## Commands and controls

| Command / key                        | Who         | What it does                                                                             |
| ------------------------------------ | ----------- | ---------------------------------------------------------------------------------------- |
| `/dealeradmin`                       | admins      | Opens the admin panel (name set in `Config.AdminCommand`)                                |
| `G`                                  | test driver | Ends the test drive early (`Config.TestDrive.endKey`)                                    |
| `E` / `Backspace` / arrows / `Shift` | staff       | Confirm, cancel, rotate and fine rotate when placing a showroom car (`Config.PlaceKeys`) |

Admins are players in `Config.AdminGroups` or with the ACE permission `lvl_dealership.admin`:

```
add_ace group.admin lvl_dealership.admin allow
```

## Admin panel

`/dealeradmin` opens one panel for everything. Pick a dealership first, then:

| Page           | What you can do                                                                                                                                                   |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Overview       | Sales today and in 7 days, company money, open loans                                                                                                              |
| Settings       | Name, type, job, positions (ped, spawn, boss laptop, sell point, test drive routes, delivery), blip, license, currency. Positions are taken from where you stand. |
| Catalog        | Add, edit and delete cars and categories, price, purchase price, stock, change all prices by %, copy the catalog to another dealership                            |
| Orders         | See open stock orders, complete or cancel them (the company gets a refund for cars not delivered)                                                                 |
| Loans          | Search loans, postpone a payment, forgive the rest, repossess the car                                                                                             |
| Sales          | Sales log with search                                                                                                                                             |
| Discount codes | Codes of the picked dealership                                                                                                                                    |
| Webhooks       | Discord webhook per dealership and per event, with a test button                                                                                                  |
| Tools          | Give a car to a player, trailer slot preview, reload showroom                                                                                                     |

Every change is saved to the database and applied at once.

## Configuration

All options are in `config.lua`. Secrets are in `server/config.lua`.

### General

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

### Company vehicles

```lua
Config.JobVehicleColumn = nil      -- column in your vehicles table for the job, e.g. 'job'
Config.JobGradeColumn = nil        -- column for the min. grade, e.g. 'grade'
Config.CompanyBuyGrades = { 'boss' }   -- grades that may buy cars for the job
```

Without `JobVehicleColumn` a car bought for the company is saved as a normal owned car.

### Financing

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

### Colours

```lua
Config.Colors = {
    mode = 'rgb',     -- 'rgb' | 'palette' | 'gta' | false (no colour step)
    palette = { { label = 'White', hex = '#F2F2F2' }, ... },
    gta = { { id = 0, label = 'Metallic Black', hex = '#0D1116' }, ... },
}
```

| Mode      | Result                                                                          |
| --------- | ------------------------------------------------------------------------------- |
| `rgb`     | Full colour picker                                                              |
| `palette` | Only your colours from `palette`                                                |
| `gta`     | GTA paints from `gta` (`id` = paint index, `hex` = swatch colour in the tablet) |
| `false`   | No colour step, the car keeps its default colour                                |

### Extras

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

### Test drive

```lua
Config.TestDrive = {
    duration = 90,          -- seconds
    endKey = 47,            -- G
    plate = 'TEST',
    privateWorld = true,    -- own routing bucket, nobody gets in the way
    damageFee = 500,        -- max fee for a wrecked car, scaled by damage
}
```

### Stock orders

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

### Discord logs

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

### server/config.lua

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

## Items

| Item            | Needed   | Use                                                                                                   |
| --------------- | -------- | ----------------------------------------------------------------------------------------------------- |
| `discount_code` | optional | Voucher with a discount code. Staff give it from the tablet, the code fills in when the buyer has it. |

## Database

Created automatically. `INSTALL/lvl_dealership.sql` only if your database user cannot create tables.

| Table                         | Content                           |
| ----------------------------- | --------------------------------- |
| `lvl_dealership_locations`    | Dealerships                       |
| `lvl_dealership_vehicles`     | Catalog                           |
| `lvl_dealership_categories`   | Categories                        |
| `lvl_dealership_showroom`     | Showroom cars                     |
| `lvl_dealership_codes`        | Discount codes                    |
| `lvl_dealership_finance`      | Loans                             |
| `lvl_dealership_sales`        | Sales log                         |
| `lvl_dealership_orders`       | Stock orders                      |
| `lvl_dealership_transactions` | Company transactions              |
| `lvl_dealership_settings`     | Name and logo per dealership      |
| `lvl_dealership_webhooks`     | Webhooks per dealership and event |

Bought vehicles are saved to the vehicles table of your framework (`owned_vehicles` on ESX, `player_vehicles` on QBCore and Qbox).

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>The car spawns without keys or fuel</summary>

Add your keys and fuel export to `Config.OnVehicleSpawned` in `config.lua`.

</details>

<details>

<summary>Boat or air shop says I need a license</summary>

The starter Boat Shop needs license `boat` and the Air Shop license `aircraft`. Give the license with your license or school script, or remove it on the Settings page in `/dealeradmin`.

</details>

<details>

<summary>I cannot order a car for stock</summary>

Only `owned` dealerships order stock, and only cars with a stock number in the catalog. Empty stock means unlimited.

</details>

<details>

<summary>The delivery trucks never come</summary>

A staff member must be within `Config.Orders.hostDistance` of the dealership, and the dealership needs `delivery.from` and `delivery.unload` on its Settings page.

</details>

<details>

<summary>Where are the dealerships in config.lua?</summary>

They are in the database. Use `/dealeradmin`. `server/starter.lua` is only used on the very first start.

</details>
