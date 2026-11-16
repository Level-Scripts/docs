---
description: >-
  Place an RC car from your inventory and drive it with a controller. Add a
  camera, microphone, antenna and swap batteries.
icon: gamepad-modern
cover: ../../.gitbook/assets/cover_lvl_rccar.png
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

# lvl\_rccar

[Buy on Tebex](https://level-scripts.tebex.io/package/rccar) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Place and drive RC cars with a controller
* Camera with normal, night vision and thermal mode
* Microphone and antenna upgrades
* Battery that drains, swappable
* Every car is an item with its own name and parts
* Job lock per model
* Shop with blip

## Requirements

| Resource                                                                      |                        |
| ----------------------------------------------------------------------------- | ---------------------- |
| [lvl\_core](../../lvl_core/)                                                  | required               |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)             | required               |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest)            | required               |
| Framework | ESX Legacy, QBCore, Qbox, ND Core, ox\_core |
| Inventory | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory |
| ox\_target or qb-target                                                       | required               |

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).

{% hint style="info" %}
With ox\_inventory the shop is the ox\_inventory shop. Other inventories get a built-in buy menu.
{% endhint %}
