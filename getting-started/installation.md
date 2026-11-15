---
description: How to download and start any Level Scripts resource.
---

# Installation

## 1. Download

After the purchase the script is added to your [Cfx.re Portal](https://portal.cfx.re/assets/granted-assets) under **Granted Assets**. Download it there with the same account that owns your server key. Free scripts are claimed on [Tebex](https://level-scripts.tebex.io/) and appear in the same place.

Download [lvl\_core](lvl_core.md) too. Every Level Scripts resource needs it.

{% hint style="warning" %}
Do not rename the resource folders. The scripts find each other by name (`lvl_core`, `lvl_dealership`...).
{% endhint %}

## 2. Requirements

These are needed by every script:

* A server with **OneSync** turned on
* [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)
* [lvl\_core](lvl_core.md)
* [oxmysql](https://github.com/overextended/oxmysql/releases/latest) for scripts that save data

Extra requirements are listed on the page of each script.

## 3. server.cfg order

The order matters. lvl\_core has to start **after** your framework, inventory, target and UI resources and **before** every lvl script.

```
ensure oxmysql
ensure ox_lib

# your framework, one of them
ensure es_extended        # or qb-core / qbx_core / ND_Core / ox_core

# your inventory and target
ensure ox_inventory
ensure ox_target

ensure lvl_core

ensure lvl_dealership
ensure lvl_motel
# ...other lvl scripts
```

## 4. Database

You do not need to import SQL. Every script creates its own tables on the first start. All table names start with the script name (`lvl_dealership_...`, `lvl_motel_...`), so they never clash with other resources.

If your database user is not allowed to create tables, run the `.sql` file from the `INSTALL` folder of the script once.

## 5. Items

Scripts that use items have the item list in their `INSTALL` folder, ready to paste into `ox_inventory/data/items.lua` (some scripts also include a QBCore version). The exact items are listed on the page of each script.

## 6. Start the server

Start the server and read the console. Every script prints one line when it starts:

```
[lvl_dealership] v2.3.0 – Level Scripts
```

When a newer version exists, the console tells you right below it.

lvl\_core also prints what it detected:

```
[lvl_core] Framework: esx | Inventory: ox_inventory | Notify: ox_lib | Progress: ox_lib | Text UI: ox_lib | Target: ox_target
```

If you see a **WARNING** or **ERROR** there, read [lvl\_core](lvl_core.md#auto-detection).

## 7. Admin permission

Admin features (for example `/dealeradmin`) work with your framework admin groups. On any framework you can also give the ACE permission:

```
add_ace group.admin lvl.admin allow
```

## Editable files

Scripts are protected by the Cfx.re asset escrow. Everything you need to change stays open:

* `config.lua` and `server/config.lua`
* `locales/*.json`
* bridge files and files called `editable.lua`
* the `INSTALL` folder
