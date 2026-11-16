---
description: >-
  Car, boat and air dealerships with test drives, financing, a used car lot,
  player run companies and stock delivery trucks. Everything is managed in game
  with /dealeradmin.
icon: car
cover: ../../.gitbook/assets/cover_lvl_dealership.png
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

# lvl\_dealership

[Buy on Tebex](https://level-scripts.tebex.io/package/dealership) | [Discord](https://www.discord.gg/UKqwhpjczw)

## Features

* Self-service shops, player owned companies and a used car lot
* Catalog tablet with search, specs and compare
* Showroom cars placed in game
* Test drives in a private world
* Colours: RGB, own palette or GTA paints
* Custom plates with a blocked word list
* Financing with interest, payoff and repossession
* Discount codes and voucher items
* Return window and sell back
* Boss tablet: staff, company money, statistics
* Stock orders delivered by NPC trucks
* Company vehicles and custom currency
* Admin panel `/dealeradmin` for everything
* Discord logs per dealership and event

## Requirements

| Resource                                                           |                                            |
| ------------------------------------------------------------------ | ------------------------------------------ |
| [lvl\_core](../../lvl_core/)                                       | required                                   |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)  | required                                   |
| [oxmysql](https://github.com/overextended/oxmysql/releases/latest) | required                                   |
| Framework | ESX Legacy, QBCore, Qbox, ND Core, ox\_core |
| Inventory | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory or your framework's own inventory (trunk info only with ox\_inventory) |
| ox\_target or qb-target                                            | optional, text UI prompts without it       |

Framework and inventory are detected automatically, you can set them in [lvl\_core configuration](../../lvl_core/configuration.md).
