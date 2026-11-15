---
description: >-
  Police seal a suspect's items into a labeled evidence bag and give them back
  later. Every bag is its own stash.
---

# lvl\_evidencebag

[Get it on Tebex](https://level-scripts.tebex.io/package/evidence-bag) | [Discord](https://www.discord.gg/UKqwhpjczw)

An officer uses an empty evidence bag on a nearby player and all their items go into the bag. The full bag is one item in the officer's inventory with a label and the owner's name. It can be opened, labeled, stored in the evidence locker and given back to the owner at any time.

## Features

* **One click** confiscation of all items of a nearby player
* **Prohibited items** stay with the player (food, water...)
* **Labeled bags**: random case number, custom label, owner name in the description
* **Open the bag** like a stash, add or remove evidence
* **Give back**: return the items to any nearby player, what does not fit stays in the bag
* Bags survive restarts, the bag ID cannot be guessed by other players
* Job and distance are checked on the server
* English and Czech, every text editable

## Requirements

| Resource | |
| --- | --- |
| [lvl\_core](../lvl_core.md) | required |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required |
| [ox\_inventory](https://github.com/overextended/ox_inventory/releases/latest) | required (stashes and item buttons) |
| Framework | any supported by lvl\_core |

## Installation

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

## How to use

| Action | How |
| --- | --- |
| Confiscate | Use an **empty bag**, pick the nearby player. Their items go into a new full bag. |
| Open | Use the **full bag**. It opens as a stash. |
| Label | Right click the full bag, **Set label** (3 to 30 characters). |
| Give back | Right click the full bag, **Unpack**, pick the nearby player. |

## Configuration

```lua
Config.Policejobs = { 'police', 'sheriff' }   -- jobs that can use evidence bags

Config.EBItems = {
    full = 'evidence_bag_full',
    empty = 'evidence_bag_empty',
}

Config.EBLabelPrefix = 'EB - '   -- start of every bag label

Config.MaxDistance = 3.0         -- metres between officer and player

Config.Stash = { slots = 50, weight = 50000 }   -- size of one bag (grams)

-- items that stay with the player
Config.ProhibitedItems = {
    'water',
    'sandwich',
    'burger',
    'cola',
    'apple',
}
```

## Items

| Item | Use |
| --- | --- |
| `evidence_bag_empty` | Confiscate the items of a nearby player |
| `evidence_bag_full` | The sealed bag with the items, label and owner |

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>Set label and Unpack buttons are missing</summary>

The `buttons` part of `evidence_bag_full` is missing in your `items.lua`. Copy the item from `INSTALL/ox_items.txt` and restart ox\_inventory.

</details>

<details>

<summary>The player has nothing to put in the bag</summary>

All their items are in `Config.ProhibitedItems`, or the player has an empty inventory.

</details>
