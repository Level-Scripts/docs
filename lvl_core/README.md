---
description: >-
  Free shared library for every Level Scripts resource. One config for
  framework, inventory, target, notifications, progress bar, text UI and menus.
cover: ../.gitbook/assets/cover_lvl_core.png
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

# lvl\_core

## Supported

| Category          | Supported                                                                                                                                                                             | Config            |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| Framework         | ESX Legacy, QBCore, Qbox, ND Core, ox\_core, standalone                                                                                                                               | `Framework`       |
| Inventory         | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory, framework items                         | `Inventory`       |
| Target            | ox\_target, qb-target, none (text UI prompts)                                                                                                                                         | `Target`          |
| Notifications     | ox\_lib, okokNotify, brutal\_notify, wasabi\_notify, lation\_ui, codem-notification, mythic\_notify, pNotify, t-notify, k5\_notify, vms\_notify, Qbox, QBCore, ESX, GTA, chat, custom | `Notify.system`   |
| Progress bar      | ox\_lib (bar or circle), lation\_ui, esx\_progressbar, QBCore progressbar, mythic\_progbar, rprogress, progressBars, none, custom                                                     | `Progress.system` |
| Text UI           | ox\_lib, okokTextUI, jg-textui, cd\_drawtextui, brutal\_textui, lation\_ui, QBCore, ESX, GTA, custom                                                                                  | `TextUI.system`   |
| Menus and dialogs | ox\_lib, lation\_ui                                                                                                                                                                   | `Menu.system`     |
| Job money         | lvl\_banking, okokBanking, Renewed-Banking, qb-banking, qb-management, esx\_addonaccount                                                                                              | `Society`         |

## Requirements

* OneSync
* [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)
* [oxmysql](https://github.com/overextended/oxmysql/releases/latest) (only for scripts that save data)
