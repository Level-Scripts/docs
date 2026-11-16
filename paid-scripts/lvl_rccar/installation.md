# Installation

1. Put `lvl_rccar` into your resources.
2. Add it to `server.cfg` after your inventory and lvl\_core:

```
ensure your_inventory   # ox_inventory, qs-inventory, qb-inventory...
ensure lvl_core
ensure lvl_rccar
```

3. Add the items to your inventory:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua` (also in `INSTALL/ox_items.txt`):

```lua
['rcbandito'] = {
    label = 'RC Bandito',
    weight = 1500,
    stack = false,
    close = true,
    description = 'Remote controlled car',
    client = { export = 'lvl_rccar.placeRCcar' },
},

['rcminitank'] = {
    label = 'RC Tank',
    weight = 2500,
    stack = false,
    close = true,
    client = { export = 'lvl_rccar.placeRCcar' },
},

['rc_drone'] = {
    label = 'Drone',
    weight = 1200,
    stack = false,
    close = true,
    client = { export = 'lvl_rccar.placeRCcar' },
},

['rc_policedrone'] = {
    label = 'Police Drone',
    weight = 1500,
    stack = false,
    close = true,
    description = 'Police drone with thermal camera and spotlight',
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
['rc_repairkit'] = { label = 'RC Repair Kit', weight = 300, stack = true, close = true },
```
{% endtab %}

{% tab title="QBCore inventories" %}
For qb-inventory, ps-inventory, lj-inventory, qs-inventory, codem-inventory, tgiann-inventory, origen\_inventory, core\_inventory on QBCore and `framework` on QBCore add them to `qb-core/shared/items.lua` (or the items file of your inventory, same format):

```lua
['rcbandito']      = { name = 'rcbandito',      label = 'RC Bandito',    weight = 1500, type = 'item', image = 'rcbandito.png',      unique = true,  useable = true,  shouldClose = true, description = 'Remote controlled car' },
['rcminitank']     = { name = 'rcminitank',     label = 'RC Tank',       weight = 2500, type = 'item', image = 'rcminitank.png',     unique = true,  useable = true,  shouldClose = true, description = '' },
['rc_drone']       = { name = 'rc_drone',       label = 'Drone',         weight = 1200, type = 'item', image = 'rc_drone.png',       unique = true,  useable = true,  shouldClose = true, description = '' },
['rc_policedrone'] = { name = 'rc_policedrone', label = 'Police Drone',  weight = 1500, type = 'item', image = 'rc_policedrone.png', unique = true,  useable = true,  shouldClose = true, description = 'Police drone with thermal camera and spotlight' },
['controller']     = { name = 'controller',     label = 'RC Controller', weight = 300,  type = 'item', image = 'controller.png',     unique = true,  useable = true,  shouldClose = true, description = 'Drive your placed RC cars' },
['rc_camera']      = { name = 'rc_camera',      label = 'RC Camera',     weight = 100,  type = 'item', image = 'rc_camera.png',      unique = false, useable = false, shouldClose = true, description = '' },
['rc_microphone']  = { name = 'rc_microphone',  label = 'RC Microphone', weight = 50,   type = 'item', image = 'rc_microphone.png',  unique = false, useable = false, shouldClose = true, description = '' },
['rc_antenna']     = { name = 'rc_antenna',     label = 'RC Antenna',    weight = 80,   type = 'item', image = 'rc_antenna.png',     unique = false, useable = false, shouldClose = true, description = '' },
['rc_battery']     = { name = 'rc_battery',     label = 'RC Battery',    weight = 200,  type = 'item', image = 'rc_battery.png',     unique = true,  useable = false, shouldClose = true, description = '' },
['rc_repairkit']   = { name = 'rc_repairkit',   label = 'RC Repair Kit', weight = 300,  type = 'item', image = 'rc_repairkit.png',   unique = false, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ESX (database)" %}
The ESX default inventory (`framework`) and core\_inventory on ESX read items from the database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
    ('rcbandito', 'RC Bandito', 2),
    ('rcminitank', 'RC Tank', 3),
    ('rc_drone', 'Drone', 2),
    ('rc_policedrone', 'Police Drone', 2),
    ('controller', 'RC Controller', 1),
    ('rc_camera', 'RC Camera', 1),
    ('rc_microphone', 'RC Microphone', 1),
    ('rc_antenna', 'RC Antenna', 1),
    ('rc_battery', 'RC Battery', 1),
    ('rc_repairkit', 'RC Repair Kit', 1);
```
{% endtab %}
{% endtabs %}

4. Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).
5. Restart. The table is created automatically, cars from the old `rc_cars` table are copied once.

## Database

Created automatically. `INSTALL/lvl_rccar.sql` only if your database user cannot create tables.

| Table | Content |
| --- | --- |
| `lvl_rccar_cars` | Every RC car: owner, name, model, parts, battery, placed or not |
