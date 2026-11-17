# Installation

1. Put `lvl_rccar` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
# your framework and inventory, before lvl_core
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

On ND Core and ox\_core also add `server = { export = '<resource>.<item>' }` to every usable item, for example `server = { export = 'lvl_rccar.rcbandito' }`. With qs-inventory it works without it. Other inventories on ND Core and ox\_core are not supported for usable items (warning in the console).
{% endtab %}

{% tab title="qb-inventory" %}
`qb-core/shared/items.lua`:

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

{% tab title="ps-inventory" %}
`qb-core/shared/items.lua`:

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

{% tab title="lj-inventory" %}
`qb-core/shared/items.lua`:

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

{% tab title="qs-inventory" %}
`qs-inventory/shared/items.lua`:

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

{% tab title="codem-inventory" %}
Add them to the item list of codem-inventory (see its documentation), same format as QBCore:

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

{% tab title="core_inventory" %}
core\_inventory reads items from your framework: on ESX use the SQL below, on QBCore add them to `qb-core/shared/items.lua`.

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

{% tab title="tgiann-inventory" %}
Add them to the item list of tgiann-inventory (see its documentation), same format as QBCore:

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

{% tab title="origen_inventory" %}
Add them to the item list of origen\_inventory (see its documentation), same format as QBCore:

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

{% tab title="framework" %}
Old ESX inventory: the SQL below. Old QBCore inventory: `qb-core/shared/items.lua`.

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

* `lvl_rccar_cars`: Every RC car: owner, name, model, parts, battery, placed or not
