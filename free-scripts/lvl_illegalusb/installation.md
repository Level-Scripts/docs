# Installation

1. Put `lvl_illegalusb` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_illegalusb
```

3. Add the items:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua` (also in `INSTALL/ox_items.txt`):

```lua
['usb_lockpick'] = { label = 'Lockpick', weight = 160 },

['usb_blue']   = { label = 'USB Blue',   weight = 10, stack = true, close = true },
['usb_green']  = { label = 'USB Green',  weight = 10, stack = true, close = true },
['usb_pink']   = { label = 'USB Pink',   weight = 10, stack = true, close = true },
['usb_purple'] = { label = 'USB Purple', weight = 10, stack = true, close = true },
['usb_red']    = { label = 'USB Red',    weight = 10, stack = true, close = true },
['usb_yellow'] = { label = 'USB Yellow', weight = 10, stack = true, close = true },
```

On ND Core and ox\_core also add `server = { export = '<resource>.<item>' }` to every usable item, for example `server = { export = 'lvl_illegalusb.usb_blue' }`.
{% endtab %}

{% tab title="QBCore inventories" %}
For qb-inventory, ps-inventory, lj-inventory, qs-inventory, codem-inventory, tgiann-inventory, origen\_inventory, core\_inventory on QBCore and `framework` on QBCore add them to `qb-core/shared/items.lua` (or the items file of your inventory, same format). Also in `INSTALL/qb_items.txt`:

```lua
['usb_lockpick'] = { name = 'usb_lockpick', label = 'Lockpick', weight = 160, type = 'item', image = 'usb_lockpick.png', unique = false, useable = false, shouldClose = true, description = '' },

['usb_blue']   = { name = 'usb_blue',   label = 'USB Blue',   weight = 10, type = 'item', image = 'usb_blue.png',   unique = false, useable = true, shouldClose = true, description = '' },
['usb_green']  = { name = 'usb_green',  label = 'USB Green',  weight = 10, type = 'item', image = 'usb_green.png',  unique = false, useable = true, shouldClose = true, description = '' },
['usb_pink']   = { name = 'usb_pink',   label = 'USB Pink',   weight = 10, type = 'item', image = 'usb_pink.png',   unique = false, useable = true, shouldClose = true, description = '' },
['usb_purple'] = { name = 'usb_purple', label = 'USB Purple', weight = 10, type = 'item', image = 'usb_purple.png', unique = false, useable = true, shouldClose = true, description = '' },
['usb_red']    = { name = 'usb_red',    label = 'USB Red',    weight = 10, type = 'item', image = 'usb_red.png',    unique = false, useable = true, shouldClose = true, description = '' },
['usb_yellow'] = { name = 'usb_yellow', label = 'USB Yellow', weight = 10, type = 'item', image = 'usb_yellow.png', unique = false, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ESX (database)" %}
The ESX default inventory (`framework`) and core\_inventory on ESX read items from the database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
    ('usb_lockpick', 'Lockpick', 1),
    ('usb_blue', 'USB Blue', 1),
    ('usb_green', 'USB Green', 1),
    ('usb_pink', 'USB Pink', 1),
    ('usb_purple', 'USB Purple', 1),
    ('usb_red', 'USB Red', 1),
    ('usb_yellow', 'USB Yellow', 1);
```
{% endtab %}
{% endtabs %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).

4. Connect your hacking minigame (`client/editable.lua`), lockpick minigame and dispatch (`config.lua`).
5. Put the USBs into your shops, loot tables or crafting.
