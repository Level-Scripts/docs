# Installation

1. Put `lvl_evidencebag` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
# your framework and inventory, before lvl_core
ensure lvl_core
ensure lvl_evidencebag
```

3. Add the items to your inventory:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua` (also in `INSTALL/ox_items.txt`):

```lua
['evidence_bag_empty'] = {
    label = 'Empty Evidence Bag',
    weight = 100,
    stack = true,
    close = true,
},

['evidence_bag_full'] = {
    label = 'Evidence Bag',
    weight = 0,
    stack = false,
    close = true,
    buttons = {
        {
            label = 'Set label',
            action = function(slot)
                TriggerEvent('lvl_evidence:renameEvidenceBag', slot)
            end,
        },
        {
            label = 'Unpack',
            action = function(slot)
                TriggerEvent('lvl_evidence:unpackSelect', slot)
            end,
        },
    },
},
```

On ND Core and ox\_core also add `server = { export = '<resource>.<item>' }` to every usable item, for example `server = { export = 'lvl_evidencebag.evidence_bag_empty' }`. With qs-inventory it works without it. Other inventories on ND Core and ox\_core are not supported for usable items (warning in the console).
{% endtab %}

{% tab title="qb-inventory" %}
`qb-core/shared/items.lua`:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ps-inventory" %}
`qb-core/shared/items.lua`:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="lj-inventory" %}
`qb-core/shared/items.lua`:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="qs-inventory" %}
`qs-inventory/shared/items.lua`:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="codem-inventory" %}
Add them to the item list of codem-inventory (see its documentation), same format as QBCore:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="core_inventory" %}
core\_inventory reads items from your framework: on ESX use the SQL below, on QBCore add them to `qb-core/shared/items.lua`.

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
    ('evidence_bag_empty', 'Empty Evidence Bag', 1),
    ('evidence_bag_full', 'Evidence Bag', 1);
```
{% endtab %}

{% tab title="tgiann-inventory" %}
Add them to the item list of tgiann-inventory (see its documentation), same format as QBCore:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="origen_inventory" %}
Add them to the item list of origen\_inventory (see its documentation), same format as QBCore:

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}
{% endtabs %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).

4. Give `evidence_bag_empty` to your police (armory or shop).
