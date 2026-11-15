# Configuration

## config.lua

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

## Levels

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

## Drugs

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

## Street NPCs

```lua
Config.BlacklistPeds = { "a_c_cow", "a_c_boar", "a_c_husky1", "s_m_m_migrant_01", "a_c_deer" }
```

## Delivery

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

## Vending machines

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

## Dispatch

Called on the client when a buyer calls the police. Default is cd\_dispatch, replace it with your dispatch:

```lua
Config.Dispatch = function()
    -- your dispatch export or event here
end
```

## server/config.lua

```lua
Config.Webhook = ""   -- Discord webhook for logs, "" = off
```
