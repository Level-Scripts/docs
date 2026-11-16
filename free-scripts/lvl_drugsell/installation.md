# Installation

1. Put `lvl_drugsell` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_drugsell
```

3. Add the vending machine item:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua`:

```lua
['drug_machine'] = {
    label = 'Vending machine',
    weight = 25000,
    stack = false,
    close = true,
},
```
{% endtab %}

{% tab title="QBCore inventories" %}
For qb-inventory, ps-inventory, lj-inventory, qs-inventory, codem-inventory, tgiann-inventory, origen\_inventory, core\_inventory on QBCore and `framework` on QBCore add it to `qb-core/shared/items.lua` (or the items file of your inventory, same format). Also in `INSTALL/qb_item.txt`:

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ESX (database)" %}
The ESX default inventory (`framework`) and core\_inventory on ESX read items from the database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('drug_machine', 'Vending machine', 25);
```
{% endtab %}
{% endtabs %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).

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
