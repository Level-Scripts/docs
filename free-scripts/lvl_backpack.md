---
description: >-
  Bags from the clothing menu add inventory slots and weight. Take the bag off
  and the inventory gets smaller again.
icon: backpack
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: hero
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# lvl\_backpack

[Get it on Tebex](https://level-scripts.tebex.io/package/backpack-system) | [Discord](https://www.discord.gg/UKqwhpjczw)

The bag a player wears decides how much they can carry. Put on a backpack in the clothing store and the inventory gets more slots and weight. Take it off and it goes back to the base size. No extra items and no menus, it simply follows the clothes.

## Features

* Any clothing bag (or other clothing piece) can add **slots and weight**
* Works with any clothing script, it reads what the player wears
* **Items are never lost**: when a smaller bag would hide items, the slots stay until the player moves them
* Updates on join, relog and every clothing change
* Server sets the size, players cannot pick their own
* State bag `clothBackpack` for other scripts (true when a bag is worn)
* English and Czech, every text editable

## Requirements

| Resource                                                          |                                                                                           |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [lvl\_core](../lvl_core.md)                                       | required                                                                                  |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required                                                                                  |
| An inventory that supports changing slots and weight              | [ox\_inventory](https://github.com/overextended/ox_inventory/releases/latest) recommended |
| Framework                                                         | any supported by lvl\_core                                                                |

## Installation

1. Put `lvl_backpack` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_backpack
```

3. Set the base inventory size and your bags in `config.lua`.

## Configuration

```lua
-- inventory size without a bag
Config.DefaultInventory = {
    slots = 50,
    weight = 24000,   -- grams
}

-- slots and weight ADDED to DefaultInventory while the piece is worn
Config.ClothesBackpacks = {
    { component = 5, drawable = 40, slots = 10, weight = 8000 },
    { component = 5, drawable = 41, slots = 10, weight = 8000 },
    { component = 5, drawable = 44, slots = 12, weight = 10000 },
    { component = 5, drawable = 45, slots = 12, weight = 10000 },
    { component = 5, drawable = 81, slots = 14, weight = 12000 },
    { component = 5, drawable = 82, slots = 14, weight = 12000 },
    { component = 5, drawable = 85, slots = 15, weight = 15000 },
    { component = 5, drawable = 86, slots = 15, weight = 15000 },
    { component = 4, drawable = 102, slots = 4, weight = 2000 },
}
```

| Field       | Meaning                                                |
| ----------- | ------------------------------------------------------ |
| `component` | Clothing slot: `5` = bags, `4` = legs, `11` = torso... |
| `drawable`  | Number of the clothing piece in that slot              |
| `slots`     | Slots added                                            |
| `weight`    | Grams added                                            |

{% hint style="info" %}
Set `DefaultInventory` to the same size your inventory uses for players (for ox\_inventory `inventory:slots` and `inventory:weight`), otherwise players without a bag get a different size.
{% endhint %}

### Find the drawable number

Open your clothing menu, go to **Bags** and pick the bag. The number shown next to it is the `drawable`. Pants pockets or vests work the same way with their own `component`.

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>The inventory size does not change</summary>

Your inventory must support changing slots and weight per player. ox\_inventory does. Check the `[lvl_core]` start line for the detected inventory.

</details>

<details>

<summary>I took off the bag but still have more slots</summary>

Some items are still in the slots of the bag. Move them to the lower slots and the inventory shrinks within a few seconds.

</details>
