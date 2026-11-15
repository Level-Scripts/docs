---
description: The most common problems and how to fix them.
---

# Troubleshooting

## The script does not start

* **`Could not find dependency lvl_core`**: lvl\_core is missing or starts after the script. Put `ensure lvl_core` above every lvl script in `server.cfg`.
* **`Could not find dependency ox_lib` / `oxmysql`**: install them and start them before lvl\_core.
* **`You lack the required entitlement`**: the script was downloaded with a different Cfx.re account than the one that owns the server key. Download it again from the [Portal](https://portal.cfx.re/assets/granted-assets) of the right account.

## Wrong framework, inventory or notifications

Read the `[lvl_core]` line in the server console after start.

* **WARNING**: lvl\_core found more than one option (for example two inventories) and took the first one. Set the right value in `lvl_core/config.lua`, the warning tells you which.
* **ERROR**: the value in `lvl_core/config.lua` is not running or not supported. lvl\_core falls back to auto detection.

Type `/lvlcore` in the server console to print the detection again. See [lvl\_core](lvl_core.md#auto-detection).

## Items do not work

* The item is not in `ox_inventory/data/items.lua`. Copy it from the `INSTALL` folder of the script and restart ox\_inventory.
* The item name in the config of the script is different from the name in your inventory. They must match.

## Texts show as keys (for example `rent_room`)

The `locales` folder is missing or the JSON has an error (a missing comma or quote). Check the file in a JSON validator. See [Language](language.md).

## Tables are not created

Your database user cannot create tables. Run the `.sql` file from the `INSTALL` folder of the script once, then restart.

## Still stuck?

Open a ticket on our [Discord](https://www.discord.gg/UKqwhpjczw). Send:

* the full error from the server console (F8 for client errors)
* the `[lvl_core]` detection line
* your framework and inventory
