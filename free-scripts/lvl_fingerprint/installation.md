# Installation

1. Put `lvl_fingerprint` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_fingerprint
```

3. Pick how officers open the scanner in `Config.InteractMethod`.
4. Put your department logos into `html/img/` and set them in `Config.LawEnforcements`.
5. For `InteractMethod = 'item'`, add the item to your inventory:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua`:

```lua
['fingerprint'] = {
    label = 'Fingerprint Scanner',
    weight = 300,
    stack = false,
    close = true,
},
```
{% endtab %}

{% tab title="QBCore inventories" %}
For qb-inventory, ps-inventory, lj-inventory, qs-inventory, codem-inventory, tgiann-inventory, origen\_inventory, core\_inventory on QBCore and `framework` on QBCore add it to `qb-core/shared/items.lua` (or the items file of your inventory, same format):

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ESX (database)" %}
The ESX default inventory (`framework`) and core\_inventory on ESX read items from the database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('fingerprint', 'Fingerprint Scanner', 1);
```
{% endtab %}
{% endtabs %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).
