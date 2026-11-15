# FAQ

<details>

<summary>The car spawns without keys or fuel</summary>

Add your keys and fuel export to `Config.OnVehicleSpawned` in `config.lua`.

</details>

<details>

<summary>Boat or air shop says I need a license</summary>

The starter Boat Shop needs license `boat` and the Air Shop license `aircraft`. Give the license with your license or school script, or remove it on the Settings page in `/dealeradmin`.

</details>

<details>

<summary>I cannot order a car for stock</summary>

Only `owned` dealerships order stock, and only cars with a stock number in the catalog. Empty stock means unlimited.

</details>

<details>

<summary>The delivery trucks never come</summary>

A staff member must be within `Config.Orders.hostDistance` of the dealership, and the dealership needs `delivery.from` and `delivery.unload` on its Settings page.

</details>

<details>

<summary>Where are the dealerships in config.lua?</summary>

They are in the database. Use `/dealeradmin`. `server/starter.lua` is only used on the very first start.

</details>
