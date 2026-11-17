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

On ND Core and ox\_core also add `server = { export = 'lvl_drugsell.drug_machine' }` to the item. With qs-inventory it works without it. Other inventories on ND Core and ox\_core are not supported for usable items (warning in the console).
{% endtab %}

{% tab title="qb-inventory" %}
`qb-core/shared/items.lua` (also in `INSTALL/qb_item.txt`):

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ps-inventory" %}
`qb-core/shared/items.lua` (also in `INSTALL/qb_item.txt`):

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="lj-inventory" %}
`qb-core/shared/items.lua` (also in `INSTALL/qb_item.txt`):

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="qs-inventory" %}
`qs-inventory/shared/items.lua`:

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="codem-inventory" %}
Add it to the item list of codem-inventory (see its documentation), same format as QBCore:

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="core_inventory" %}
core\_inventory reads items from your framework: on ESX use the SQL below, on QBCore add it to `qb-core/shared/items.lua`.

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('drug_machine', 'Vending machine', 25);
```
{% endtab %}

{% tab title="tgiann-inventory" %}
Add it to the item list of tgiann-inventory (see its documentation), same format as QBCore:

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="origen_inventory" %}
Add it to the item list of origen\_inventory (see its documentation), same format as QBCore:

```lua
['drug_machine'] = { name = 'drug_machine', label = 'Vending machine', weight = 25000, type = 'item', image = 'drug_machine.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="framework" %}
Old ESX inventory: the SQL below. Old QBCore inventory: `qb-core/shared/items.lua`.

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
