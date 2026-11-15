# Installation

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

## Database

Created automatically. `INSTALL/lvl_rccar.sql` only if your database user cannot create tables.

| Table | Content |
| --- | --- |
| `lvl_rccar_cars` | Every RC car: owner, name, model, parts, battery, placed or not |
