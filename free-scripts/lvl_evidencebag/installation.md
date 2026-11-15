# Installation

1. Put `lvl_evidencebag` into your resources.
2. Add it to `server.cfg` after ox\_inventory and lvl\_core:

```
ensure ox_inventory
ensure lvl_core
ensure lvl_evidencebag
```

3. Add the items to `ox_inventory/data/items.lua` (also in `INSTALL/ox_items.txt`):

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

4. Give `evidence_bag_empty` to your police (armory or shop).
