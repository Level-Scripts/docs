# Installation

1. Put `lvl_dealership` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_dealership
```

3. Start the server. All tables are created automatically. On the first start the starter dealerships from `server/starter.lua` are copied into the database once.
4. Join the game and open `/dealeradmin` to check the dealerships and add vehicles to the catalog.
5. Optional, for discount vouchers, add the item to your inventory:

{% tabs %}
{% tab title="ox_inventory" %}
`ox_inventory/data/items.lua`:

```lua
['discount_code'] = {
    label = 'Discount voucher',
    weight = 10,
    stack = false,
},
```
{% endtab %}

{% tab title="qb-inventory" %}
`qb-core/shared/items.lua`:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="ps-inventory" %}
`qb-core/shared/items.lua`:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="lj-inventory" %}
`qb-core/shared/items.lua`:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="qs-inventory" %}
`qs-inventory/shared/items.lua`:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="codem-inventory" %}
Add it to the item list of codem-inventory (see its documentation), same format as QBCore:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="core_inventory" %}
core\_inventory reads items from your framework: on ESX use the SQL below, on QBCore add it to `qb-core/shared/items.lua`.

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('discount_code', 'Discount voucher', 1);
```
{% endtab %}

{% tab title="tgiann-inventory" %}
Add it to the item list of tgiann-inventory (see its documentation), same format as QBCore:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="origen_inventory" %}
Add it to the item list of origen\_inventory (see its documentation), same format as QBCore:

```lua
['discount_code'] = { name = 'discount_code', label = 'Discount voucher', weight = 10, type = 'item', image = 'discount_code.png', unique = true, useable = false, shouldClose = true, description = '' },
```
{% endtab %}

{% tab title="framework" %}
Old ESX inventory: the SQL below. Old QBCore inventory: `qb-core/shared/items.lua`.

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES ('discount_code', 'Discount voucher', 1);
```
{% endtab %}
{% endtabs %}

Copy the images from the `INSTALL` folder into the image folder of your inventory (`ox_inventory/web/images`, `qb-inventory/html/images`...).

6. Connect your car keys and fuel in `Config.OnVehicleSpawned` (see [Hooks](configuration.md#hooks)).

{% hint style="info" %}
Coming from v1? Data from the old tables (vehicles, categories, showroom, codes, settings) is copied on the first start. Nothing is deleted.
{% endhint %}

## Database

Created automatically. `INSTALL/lvl_dealership.sql` only if your database user cannot create tables.

| Table | Content |
| --- | --- |
| `lvl_dealership_locations` | Dealerships |
| `lvl_dealership_vehicles` | Catalog |
| `lvl_dealership_categories` | Categories |
| `lvl_dealership_showroom` | Showroom cars |
| `lvl_dealership_codes` | Discount codes |
| `lvl_dealership_finance` | Loans |
| `lvl_dealership_sales` | Sales log |
| `lvl_dealership_orders` | Stock orders |
| `lvl_dealership_transactions` | Company transactions |
| `lvl_dealership_settings` | Name and logo per dealership |
| `lvl_dealership_webhooks` | Webhooks per dealership and event |

Bought vehicles are saved to the vehicles table of your framework (`owned_vehicles` on ESX, `player_vehicles` on QBCore and Qbox, the vehicle table of the framework on ND Core and ox\_core).
