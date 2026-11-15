---
description: >-
  Sell drugs to street NPCs, to delivery customers found by a middleman and
  through player owned vending machines. Every sale gives XP and levels.
---

# lvl\_drugsell

[Get it on Tebex](https://level-scripts.tebex.io/package/drugsell) | [Discord](https://www.discord.gg/UKqwhpjczw)

Three ways to sell drugs, each one can be switched off. Sell on the street to NPCs, let the middleman James find customers for bigger deliveries, or place a vending machine and let other players buy from it while you are away. Every sale gives XP, higher levels pay a bonus.

## Features

* **Street sales** to NPCs, switched on with a command, with sell chance and police calls
* **Delivery sales**: the middleman James finds a customer and marks the area on the GPS
* **Vending machines**: players place a machine, stock it, set names and prices, collect the money
* **Levels and XP** for every sale with a money bonus per level
* **Drug variants** by item metadata (for example a better joint sells for more)
* **Police minimum** for street and delivery sales
* **Dispatch hook** for any dispatch script
* Prices, chances and stock are checked on the server
* Discord log
* English and Czech, every text editable

## Requirements

| Resource | |
| --- | --- |
| [lvl\_core](../lvl_core.md) | required |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest) | required |
| Inventory | [ox\_inventory](https://github.com/overextended/ox_inventory/releases/latest) recommended (drug variants and machine stock use item metadata) |
| Framework | any supported by lvl\_core |

## Installation

1. Put `lvl_drugsell` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_drugsell
```

3. Add the vending machine item. ox\_inventory `data/items.lua`:

```lua
['drug_machine'] = {
    label = 'Vending machine',
    weight = 25000,
    stack = false,
    close = true,
},
```

A QBCore version is in `INSTALL/qb_item.txt`.

4. Set your drugs in `Config.Drugs` (the items must exist in your inventory).
5. Connect your dispatch in `Config.Dispatch`.
6. Optional: put a Discord webhook into `server/config.lua`.
7. Start the server. Tables are created automatically, data from the old `drug_levels` and `drug_machines` tables is copied once.

## How to use

### Street

Type `/selldrugs` to start or stop selling. Walk to an NPC and use target (or press E). Pick the drug, the NPC buys or refuses. A refusing NPC may call the police. One NPC buys only once.

### Delivery

Go to **James** (the middleman), choose **Start looking**. After a while he finds a customer and the area shows on the GPS. Bring the drugs there. Every good sale gets you a new customer. If the customer calls the police, James stops working with you.

### Vending machine

Use the `drug_machine` item and place it:

| Key | Action |
| --- | --- |
| Arrows | Move |
| Mouse wheel | Rotate |
| `E` | Place |
| `X` | Cancel |

The owner manages the machine (restock, change names and prices, withdraw money, pick it up). Other players buy from it with cash or bank. Picking up the machine returns the drugs, the money and the machine item.

## Configuration

### config.lua

```lua
Config.MoneyType = "money"     -- seller gets paid in "money", "bank" or "black_money"

Config.Interact = 'target'     -- 'target' or 'textui'
Config.PressKey = 38           -- E, for textui

Config.Minpolice = 0           -- police online needed for street and delivery sales

Config.NpcSell = true          -- street sales
Config.DeliverySell = true     -- James and delivery customers
Config.MachineSell = true      -- vending machines

Config.Command = 'selldrugs'   -- toggles street sales
```

### Levels

```lua
Config.MaxLevel = 10
Config.XPPerLevel = 2500
Config.EnableLevelBonus = true
Config.LevelMoneyBonus = {     -- money added to every street sale from this level
    [1] = 10,
    [2] = 50,
    [3] = 100,
    [4] = 200,
    [5] = 500,
}
```

### Drugs

The key is the item name. Each item has a list of variants. The variant is picked by item metadata, a variant with `metadata = nil` matches items without metadata.

```lua
Config.Drugs = {
    weed_joint = {
        {
            label = 'Joint',
            metadata = nil,
            sellChance = 80,           -- % chance the NPC buys
            maxSellCount = 2,          -- max pieces to one NPC
            prop = 'prop_sh_joint_01', -- prop in the hand
            icon = 'nui://ox_inventory/web/images/weed_joint.png',

            minPriceNPC = 500, maxPriceNPC = 700, xpNPC = 100,                -- street
            minPriceDelivery = 600, maxPriceDelivery = 900, xpDelivery = 150, -- delivery
            minPriceMachine = 0, maxPriceMachine = 1200,                     -- price range owners can set
            xpMachineBuyer = 200, xpMachineSeller = 300,                      -- machine
        },
    },
}
```

### Street NPCs

```lua
Config.BlacklistPeds = { "a_c_cow", "a_c_boar", "a_c_husky1", "s_m_m_migrant_01", "a_c_deer" }
```

### Delivery

```lua
Config.Ped = {                    -- James
    coords = vec3(-1099.14, -1258.72, 4.34),
    heading = 29.20,
    model = "a_m_m_skidrow_01",
}
Config.WaitTime = 30000           -- ms until James finds a customer
Config.CustomerModel = "a_m_m_salton_03"
Config.Location = {               -- customer spots
    vec4(-231.67, -1378.28, 30.25, 220.42),
    vec4(1442.17, -1480.83, 62.22, 349.52),
    vec4(2461.91, 989.04, 84.73, 304.35),
    vec4(1648.62, 3815.94, 33.90, 38.31),
}
```

### Vending machines

```lua
Config.MachineItem = "drug_machine"
Config.MachineMaxPlaced = 2       -- per player
Config.MachineProp = "prop_vend_snak_01"
Config.MachinePositionKey = {
    place = 38, cancel = 73,
    forward = 172, back = 173, left = 174, right = 175,
    rotationL = 14, rotationR = 15,
}
```

### Dispatch

Called on the client when a buyer calls the police. Default is cd\_dispatch, replace it with your dispatch:

```lua
Config.Dispatch = function()
    -- your dispatch export or event here
end
```

### server/config.lua

```lua
Config.Webhook = ""   -- Discord webhook for logs, "" = off
```

## Items

| Item | Use |
| --- | --- |
| `drug_machine` | Places a vending machine |
| your drug items | Everything in `Config.Drugs` |

## Database

Created automatically. `INSTALL/lvl_drugsell.sql` only if your database user cannot create tables.

| Table | Content |
| --- | --- |
| `lvl_drugsell_levels` | XP and level per character |
| `lvl_drugsell_machines` | Placed machines, owner, stock and money |

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>"You have no drugs to sell" but I have them</summary>

The item name must be a key in `Config.Drugs`, and the item metadata must match one of its variants. A variant with `metadata = nil` only takes items without metadata.

</details>

<details>

<summary>Nothing happens on police calls</summary>

`Config.Dispatch` uses cd\_dispatch by default. Put the export or event of your dispatch script there.

</details>
