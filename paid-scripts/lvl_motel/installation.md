# Installation

1. Put `lvl_motel` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
# your framework and inventory, before lvl_core
ensure lvl_core
ensure lvl_motel
```

3. Add the police item to your inventory:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua` (also in `INSTALL/ox_item.txt`):

```lua
['police_ram'] = {
    label = 'Police ram',
    weight = 8000,
    stack = false,
},
```
{% endtab %}

{% tab title="QBCore inventories" %}
For qb-inventory, ps-inventory, lj-inventory, qs-inventory, codem-inventory, tgiann-inventory, origen\_inventory, core\_inventory on QBCore and `framework` on QBCore add it to `qb-core/shared/items.lua` (or the items file of your inventory, same format):

```lua
['police_ram'] = { name = 'police_ram', label = 'Police ram', weight = 8000, type = 'item', image = 'police_ram.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ESX (database)" %}
The ESX default inventory (`framework`) and core\_inventory on ESX read items from the database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('police_ram', 'Police ram', 8);
```
{% endtab %}
{% endtabs %}

4. Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).
5. Give the `police_ram` to your police (armory, shop or job items).
6. Set motels, prices and room doors in `config/config.lua`.
7. Start the server. Tables are created automatically. Rooms from the old `motel` tables are copied once.

## Database

Created automatically. `INSTALL/lvl_motel.sql` only if your database user cannot create tables.

| Table | Content |
| --- | --- |
| `lvl_motel_rooms` | Rented rooms, tenant, rent end, lock and seal |
| `lvl_motel_keys` | Key holders and their permissions |
| `lvl_motel_inside` | Players who were inside a room when they left |

The old tables `motel`, `motel_key` and `motel_inside` from v1 are copied once and can be deleted after that.
