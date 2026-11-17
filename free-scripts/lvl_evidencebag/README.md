---
description: >-
  Police put all items of a suspect into one labeled evidence bag and give them
  back later.
icon: sack
cover: ../../.gitbook/assets/cover_lvl_evidencebag.png
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

# lvl\_evidencebag

[Get it on Tebex](https://level-scripts.tebex.io/package/evidence-bag) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Take all items of a nearby player at once
* Prohibited items stay with the player
* Labeled bags with owner name
* Open the bag like a stash
* Give the items back any time

## Requirements

* [lvl\_core](../../lvl_core/): required
* [ox\_lib](https://github.com/overextended/ox_lib/releases/latest): required
* Framework: ESX Legacy, QBCore, Qbox, ND Core, ox\_core
* Inventory: ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).

{% hint style="info" %}
Needs an inventory resource with stashes. The built-in inventory of the framework is not supported.
{% endhint %}
