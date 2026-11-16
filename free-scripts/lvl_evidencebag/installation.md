# Installation

1. Put `lvl_evidencebag` into your resources.
2. Add it to `server.cfg` after your inventory and lvl\_core:

```
ensure your_inventory   # ox_inventory, qs-inventory, qb-inventory...
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
{% endtab %}

{% tab title="QBCore inventories" %}
For qb-inventory, ps-inventory, lj-inventory, qs-inventory, codem-inventory, tgiann-inventory, origen\_inventory, core\_inventory on QBCore and `framework` on QBCore add them to `qb-core/shared/items.lua` (or the items file of your inventory, same format):

```lua
['evidence_bag_empty'] = { name = 'evidence_bag_empty', label = 'Empty Evidence Bag', weight = 100, type = 'item', image = 'evidence_bag_empty.png', unique = false, useable = true, shouldClose = true, description = '' },
['evidence_bag_full']  = { name = 'evidence_bag_full',  label = 'Evidence Bag',       weight = 0,   type = 'item', image = 'evidence_bag_full.png',  unique = true,  useable = true, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ESX (database)" %}
The ESX default inventory (`framework`) and core\_inventory on ESX read items from the database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
    ('evidence_bag_empty', 'Empty Evidence Bag', 1),
    ('evidence_bag_full', 'Evidence Bag', 1);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Opening the bag as a stash and the **Set label** and **Unpack** buttons work best on ox\_inventory.
{% endhint %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).

4. Give `evidence_bag_empty` to your police (armory or shop).
