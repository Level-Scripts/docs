# For developers

Every lvl script loads lvl\_core with two lines in its `fxmanifest.lua`:

```lua
shared_scripts {
    '@ox_lib/init.lua',
    '@lvl_core/import.lua',
    'config.lua',
}
dependency 'lvl_core'
```

The script then has the global `LVL`. It works the same on every framework.

* **Job** is the same table everywhere: `{ name, label, grade, gradeName, gradeLabel, onDuty, isBoss }`
* **Accounts**: `'money'` (cash), `'bank'`, `'black_money'`

<details>

<summary>Shared functions (client and server)</summary>

| Function | Description |
| --- | --- |
| `LVL.framework`, `LVL.inventory`, `LVL.bridge` | What is used (`'esx'`, `'ox_inventory'`, full table) |
| `LVL.core()` | Raw framework object (ESX, QBCore...) for framework specific code |
| `LVL.debug/print/warn/error(...)` | Console output, `debug` only with Debug on |
| `LVL.money(n)` | `"$12 500"` |
| `LVL.number`, `LVL.round`, `LVL.clamp`, `LVL.trim`, `LVL.split`, `LVL.shuffle`, `LVL.count`, `LVL.copy`, `LVL.dist`, `LVL.time`, `LVL.hash` | Utilities |
| `LVL.jobAllowed(jobs, name, grade)` | `{ 'police' }` or `{ police = 2 }` (min. grade) |
| `LVL.isPoliceJob(name)`, `LVL.isEmergencyJob(name)` | Checks against the config lists |
| `LVL.units()`, `LVL.speed(ms)`, `LVL.speedUnit()`, `LVL.formatSpeed`, `LVL.fromKmh`, `LVL.toKmh`, `LVL.toMs`, `LVL.distance(m)`, `LVL.distanceUnits()` | Speed and distance in the units of the player |

</details>

<details>

<summary>Server functions</summary>

| Function | Description |
| --- | --- |
| `LVL.getPlayer(src)`, `LVL.identifier(src)`, `LVL.sourceOf(identifier)`, `LVL.getPlayers()`, `LVL.getName(src)` | Player |
| `LVL.getJob(src)`, `LVL.setJob(src, name, grade)`, `LVL.hasJob(src, jobs, onDuty)`, `LVL.isPolice(src, onDuty)`, `LVL.isEmergency(src, onDuty)` | Job |
| `LVL.getGroup(src)`, `LVL.isAdmin(src)` | Admin |
| `LVL.countJobs(jobs, onDuty)`, `LVL.policeCount(onDuty)` | Players online in jobs (cached) |
| `LVL.getMoney`, `LVL.addMoney`, `LVL.removeMoney(src, account, amount, reason)`, `LVL.charge(src, amount, { 'money', 'bank' })` | Money |
| `LVL.itemCount`, `LVL.hasItem`, `LVL.canCarry`, `LVL.addItem` (returns ok, reason), `LVL.removeItem` | Inventory |
| `LVL.registerUsableItem(item, function(src, item, slot, metadata) end)` | Usable item |
| `LVL.getCharInfo(src)` | `{ firstname, lastname, dob, gender, identifier }` |
| `LVL.getItems(src, name)`, `LVL.getSlot(src, slot)`, `LVL.setMetadata(src, slot, metadata)`, `LVL.setInventorySize(src, slots, maxWeight)` | Inventory details |
| `LVL.stash.register(id, label, slots, maxWeight, owner)`, `.items(id)`, `.add`, `.remove`, `.clear(id)` | Stashes |
| `LVL.society.get(job)`, `.add(job, amount, reason)`, `.remove(job, amount, reason)` | Job money |
| `LVL.getLicenses(src)`, `LVL.hasLicense(src, type)`, `LVL.addLicense`, `LVL.removeLicense` | Licenses |
| `LVL.query/single/scalar/update/insert(sql, params)` | oxmysql shortcuts |
| `LVL.schema.players`, `LVL.schema.vehicles`, `LVL.getNameByIdentifier(id)` | Framework table and column names |
| `LVL.onPlayerLoaded(fn(src, identifier))`, `LVL.onPlayerLogout(fn(src))`, `LVL.onJobChange(fn(src, job))` | Events |
| `LVL.notify(src, text, type, title)` | Notification (`-1` = everyone) |
| `LVL.rateLimited(src, key, ms)`, `LVL.isNear(src, coords, dist)`, `LVL.coords(src)` | Event protection |
| `LVL.log(webhook or key, title, description, src, opts)` | Discord log with queue and rate limit |
| `LVL.versionCheck()` | Start line and update check |

</details>

<details>

<summary>Client functions</summary>

| Function | Description |
| --- | --- |
| `LVL.playerData()`, `LVL.isLoaded()`, `LVL.getJob()`, `LVL.hasJob(jobs, onDuty)`, `LVL.isPolice()`, `LVL.isEmergency()`, `LVL.getMoney(account)` | Player (money for display only) |
| `LVL.itemCount(item)`, `LVL.hasItem(item, count)`, `LVL.openStash(id)`, `LVL.closeInventory()` | Inventory |
| `LVL.onPlayerLoaded(fn)`, `LVL.onPlayerLogout(fn)`, `LVL.onJobChange(fn(job))` | Events |
| `LVL.notify(text, type, title or opts)` | Notification |
| `LVL.progress(label, ms, opts)` | Progress bar, returns true or false (`opts.anim`, `opts.prop`, `opts.disable`, `opts.circle`) |
| `LVL.textUI(text, opts)`, `LVL.hideTextUI()`, `LVL.isTextUIOpen()` | Text UI |
| `LVL.menu.open{ id, title, options }`, `LVL.menu.register`, `.show(id)`, `.hide()` | Context menu in ox\_lib format |
| `LVL.input(title, fields, opts)`, `LVL.confirm(header, text)`, `LVL.alert(header, text)` | Dialogs |
| `LVL.target.addSphere`, `.addBox`, `.removeZone`, `.addLocalEntity`, `.addEntity`, `.addModel`, `.addGlobalVehicle`, `.addGlobalPed`, `.addGlobalPlayer` (and `remove...`) | Target with ox\_target style options |
| `LVL.hint(text)`, `LVL.timer.show(sec, label)`, `LVL.clipboard(text)`, `LVL.chooseClosestPlayer(title)`, `LVL.closestPlayer(dist)` | UI helpers |
| `LVL.blip{...}`, `LVL.spawnPed(...)`, `LVL.spawnProp(...)` (and `remove...`), `LVL.loadModel`, `LVL.loadDict`, `LVL.playAnim`, `LVL.groundZ`, `LVL.drawText3D` | World helpers, removed when the script stops |

</details>

## Exports

For resources that do not use the import:

| Side | Exports |
| --- | --- |
| Server | `GetBridge`, `Log`, `sendToDiscord`, `CountJobs`, `GetPoliceCount`, `VersionCheck` |
| Client | `Notify`, `GetNotifySystem`, `ShowHint`, `HideHint`, `ShowTimer`, `UpdateTimer`, `HideTimer`, `Clipboard`, `ChooseClosestPlayer`, `SpawnPed`, `GetUnits`, `SetUnits` |

```lua
-- example: send a notification from any resource
exports.lvl_core:Notify({ title = 'Shop', description = 'Order ready', type = 'success' })
```

## Adding your own system

The files in `lvl_core/bridge/` are open. Each framework has its own file in `bridge/framework/`, inventories are in `bridge/inventory.lua`, target in `bridge/target.lua`, text UI in `bridge/textui.lua`. Add your resource there, or use the `custom` option in `config.lua` for notifications, progress bar and text UI.
