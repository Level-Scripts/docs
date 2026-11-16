# Configuration

Framework, inventory and target are set in [lvl\_core configuration](../../lvl_core/configuration.md).

`config.lua`:

```lua
-- item names
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

## Cars

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

## Shop

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

## Exports

Client exports used by the items:

| Export | |
| --- | --- |
| `exports.lvl_rccar:placeRCcar(data, slot)` | Places the RC car from the used item |
| `exports.lvl_rccar:useController()` | Opens the controller |
