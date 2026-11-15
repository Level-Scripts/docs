# Installation

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

## Database

Created automatically. `INSTALL/lvl_drugsell.sql` only if your database user cannot create tables.

| Table | Content |
| --- | --- |
| `lvl_drugsell_levels` | XP and level per character |
| `lvl_drugsell_machines` | Placed machines, owner, stock and money |
