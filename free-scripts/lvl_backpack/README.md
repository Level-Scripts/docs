---
description: The bag a player wears adds inventory slots and weight. No items, no menus.
icon: backpack
cover: ../../.gitbook/assets/cover_lvl_backpack.png
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

## Features

* Any clothing bag adds slots and weight
* Works with any clothing script
* Items are never lost when the bag comes off
* State bag `clothBackpack` for other scripts

## Requirements

* [lvl\_core](../../lvl_core/): required
* [ox\_lib](https://github.com/overextended/ox_lib/releases/latest): required
* Framework: ESX Legacy, QBCore, Qbox, ND Core, ox\_core
* Inventory: ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).

{% hint style="info" %}
Extra slots and weight work only with ox\_inventory. Other inventories keep their own size.
{% endhint %}
