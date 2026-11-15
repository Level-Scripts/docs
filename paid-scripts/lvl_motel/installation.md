# Installation

## Installation

1. Put `lvl_motel` into your resources.
2. Add it to `server.cfg` after ox\_inventory and lvl\_core:

```
ensure ox_inventory
ensure lvl_core
ensure lvl_motel
```

3. Add the police item to `ox_inventory/data/items.lua` (also in `INSTALL/ox_item.txt`):

```lua
['police_ram'] = {
    label = 'Police ram',
    weight = 8000,
    stack = false,
},
```

4. Copy `INSTALL/police_ram.png` to `ox_inventory/web/images/`.
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
