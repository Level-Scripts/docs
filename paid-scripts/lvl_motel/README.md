---
description: >-
  Rent a motel room at its door, share the key with friends and keep your things
  in the room stash. Police can seal and breach rooms.
icon: hotel
cover: ../../.gitbook/assets/cover_lvl_motel.png
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

# lvl\_motel

[Buy on Tebex](https://level-scripts.tebex.io/package/motel) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Rent at the door with cash or bank
* Room tour before renting
* Rent expiry with warnings
* Shared keys with permissions
* Private stash and wardrobe
* Police seal and breach
* Part of the rent to a job account
* Instanced rooms
* Discord logs

## Requirements

* [lvl\_core](../../lvl_core/): required
* [ox\_lib](https://github.com/overextended/ox_lib/releases/latest): required
* [oxmysql](https://github.com/overextended/oxmysql/releases/latest): required
* Framework: ESX Legacy, QBCore, Qbox, ND Core, ox\_core
* Inventory: ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory
* illenium-appearance, qb-clothing or esx\_skin: optional, for the wardrobe

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).

{% hint style="info" %}
The room stash needs an inventory resource with stashes. The built-in inventory of the framework is not supported.
{% endhint %}
