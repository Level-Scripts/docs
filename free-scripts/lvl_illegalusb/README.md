---
description: Hack a USB, fight the guards and crack the crate for loot.
icon: usb-drive
cover: ../../.gitbook/assets/cover_lvl_illegalusb.png
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

# lvl\_illegalusb

[Get it on Tebex](https://level-scripts.tebex.io/package/illegalusb) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Six USB tiers with own locations and loot
* Hacking and lockpick minigames, easy to replace
* Armed guards with four difficulties
* Mission timer
* Police minimum and dispatch hook

## Requirements

| Resource                                                          |                                                        |
| ----------------------------------------------------------------- | ------------------------------------------------------ |
| [lvl\_core](../../lvl_core/)                                      | required                                               |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required                                               |
| A hacking minigame                                                | default `mhacking`, change it in `client/editable.lua` |
| A lockpick minigame                                               | default `t3_lockpick`, change it in `Config.Lockpick`  |
| Framework | ESX Legacy, QBCore, Qbox, ND Core, ox\_core |
| Inventory | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory |

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).
