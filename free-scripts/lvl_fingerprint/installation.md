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

On ND Core and ox\_core also add `server = { export = 'lvl_fingerprint.fingerprint' }` to the item. With qs-inventory it works without it. Other inventories on ND Core and ox\_core are not supported for usable items (warning in the console).
{% endtab %}

{% tab title="qb-inventory" %}
`qb-core/shared/items.lua`:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ps-inventory" %}
`qb-core/shared/items.lua`:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="lj-inventory" %}
`qb-core/shared/items.lua`:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="qs-inventory" %}
`qs-inventory/shared/items.lua`:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="codem-inventory" %}
Add it to the item list of codem-inventory (see its documentation), same format as QBCore:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="core_inventory" %}
core\_inventory reads items from your framework: on ESX use the SQL below, on QBCore add it to `qb-core/shared/items.lua`.

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('fingerprint', 'Fingerprint Scanner', 1);
```
{% endtab %}

{% tab title="tgiann-inventory" %}
Add it to the item list of tgiann-inventory (see its documentation), same format as QBCore:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="origen_inventory" %}
Add it to the item list of origen\_inventory (see its documentation), same format as QBCore:

```lua
['fingerprint'] = { name = 'fingerprint', label = 'Fingerprint Scanner', weight = 300, type = 'item', image = 'fingerprint.png', unique = true, useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="framework" %}
Old ESX inventory: the SQL below. Old QBCore inventory: `qb-core/shared/items.lua`.

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('fingerprint', 'Fingerprint Scanner', 1);
```
{% endtab %}
{% endtabs %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).
