# Usage

## Starter dealerships

* **1. Premium Deluxe Motorsport**: Owned, job `pdm`, stock delivery (cars)
* **2. Boat Shop**: Self-service, needs license `boat` (boats)
* **3. Air Shop**: Self-service, needs license `aircraft` (aircraft)
* **4. Bike Shop**: Self-service (bikes)
* **5. Car Bazaar**: Used car lot, job `carbazaar` (used cars)

After the first start `server/starter.lua` is not used anymore. Create, edit and delete dealerships in `/dealeradmin`. To start over from the starter list, delete all rows of `lvl_dealership_locations` and restart.

## Dealership types

* `self-service`: A shop without employees. Players buy directly from the catalog. Stock is optional.
* `owned`: A company with a job. Employees sell, the boss manages money, staff and stock. Sales go to the company account.
* `bazaar`: Used car lot. Employees buy cars from players in the intake zone, then sell them with the same plate and tuning.

## Commands and controls

* `/dealeradmin` (admins): Opens the admin panel (name set in `Config.AdminCommand`)
* `G` (test driver): Ends the test drive early (`Config.TestDrive.endKey`)
* `E` / `Backspace` / arrows / `Shift` (staff): Confirm, cancel, rotate and fine rotate when placing a showroom car (`Config.PlaceKeys`)

Admins are players in `Config.AdminGroups` or with the ACE permission `lvl_dealership.admin`:

```
add_ace group.admin lvl_dealership.admin allow
```

## Admin panel

`/dealeradmin` opens one panel for everything. Pick a dealership first, then:

* Overview: Sales today and in 7 days, company money, open loans
* Settings: Name, type, job, positions (ped, spawn, boss laptop, sell point, test drive routes, delivery), blip, license, currency. Positions are taken from where you stand.
* Catalog: Add, edit and delete cars and categories, price, purchase price, stock, change all prices by %, copy the catalog to another dealership
* Orders: See open stock orders, complete or cancel them (the company gets a refund for cars not delivered)
* Loans: Search loans, postpone a payment, forgive the rest, repossess the car
* Sales: Sales log with search
* Discount codes: Codes of the picked dealership
* Webhooks: Discord webhook per dealership and per event, with a test button
* Tools: Give a car to a player, trailer slot preview, reload showroom

Every change is saved to the database and applied at once.

## Items

* `discount_code` (optional): Voucher with a discount code. Staff give it from the tablet, the code fills in when the buyer has it.
