# FAQ

<details>

<summary>No such export RegisterShop in resource ox_inventory</summary>

ox\_inventory had an error on start, so its shop export was never created. Fix the first ox\_inventory error in the console. lvl\_rccar retries for 30 seconds and registers the shop again when ox\_inventory restarts.

</details>

<details>

<summary>Using the item does nothing</summary>

The item needs `client = { export = 'lvl_rccar.placeRCcar' }` (car) or `client = { export = 'lvl_rccar.useController' }` (controller) in `items.lua`.

</details>
