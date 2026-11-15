# Installation

1. Put `lvl_core` into your resources folder.
2. Add it to `server.cfg` **after** your framework, inventory, target and UI resources and **before** every lvl script:

```
ensure ox_lib
ensure es_extended      # or qb-core / qbx_core / ND_Core / ox_core
ensure ox_inventory     # your inventory
ensure ox_target        # your target
ensure lvl_core
ensure lvl_dealership   # your lvl scripts
```

3. Start the server and check the console (see below).
4. Optional: give admins the ACE permission that works on every framework:

```
add_ace group.admin lvl.admin allow
```

## Auto detection

Everything is set to `'auto'` by default. On start lvl\_core looks at what is running and prints one line:

```
[lvl_core] Framework: esx | Inventory: ox_inventory | Notify: ox_lib | Progress: ox_lib | Text UI: ox_lib | Target: ox_target
```

| Message | Meaning | What to do |
| --- | --- | --- |
| **WARNING** | More than one was found (for example two inventories). lvl\_core uses the first one. | Set the value the warning shows in `config.lua`. |
| **ERROR** | The value in `config.lua` is not running or is not supported. lvl\_core falls back to auto. | Fix the value or start the resource. |
| **WARNING** resource started after lvl\_core | A framework or inventory started later than lvl\_core. | Move `ensure lvl_core` lower in `server.cfg`. |

`/lvlcore` (server console or an admin in game) prints the detection again.
