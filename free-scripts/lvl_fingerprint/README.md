---
description: Police scan the fingerprint of a player and see who they are.
icon: fingerprint
cover: ../../.gitbook/assets/cover_lvl_fingerprint.png
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

# lvl\_fingerprint

[Get it on Tebex](https://level-scripts.tebex.io/package/7364003) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Two sided scan, the player can refuse
* Name, date of birth, gender, BOLO
* Scan history
* Logo and colour per department
* Open with target, item or command

## Requirements

| Resource                                                          |                                      |
| ----------------------------------------------------------------- | ------------------------------------ |
| [lvl\_core](../../lvl_core/)                                      | required                             |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required                             |
| ox\_target or qb-target                                           | only for `InteractMethod = 'target'` |
| Framework | ESX Legacy, QBCore, Qbox, ND Core, ox\_core |
| Inventory | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory (only for `InteractMethod = 'item'`) |

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).
