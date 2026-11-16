---
description: >-
  Sell drugs to street NPCs, to delivery customers or through your own vending
  machine. Every sale gives XP.
icon: capsule
cover: ../../.gitbook/assets/cover_lvl_drugsell.png
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

# lvl\_drugsell

[Get it on Tebex](https://level-scripts.tebex.io/package/drugsell) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Street sales to NPCs
* Delivery customers through a middleman
* Player owned vending machines
* Levels with a money bonus
* Drug variants by metadata
* Police minimum and dispatch hook

## Requirements

| Resource                                                           |                                                                                                                                               |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| [lvl\_core](../../lvl_core/)                                       | required                                                                                                                                      |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)  | required                                                                                                                                      |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest) | required                                                                                                                                      |
| Framework | ESX Legacy, QBCore, Qbox, ND Core, ox\_core |
| Inventory | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory (drug variants and machine stock use item metadata) |

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).
