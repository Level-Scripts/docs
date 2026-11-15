---
description: >-
  Free shared library for every Level Scripts resource. One config for
  framework, inventory, target, notifications, progress bar, text UI and menus.
---

# lvl\_core

lvl\_core is the base of every Level Scripts resource. It is **free** and comes with every purchase. It connects our scripts to your server: framework, inventory, target, notifications, progress bar, text UI, menus and job money. You set it up once and every lvl script follows it.

## Supported resources

| Category | Supported | Config |
| --- | --- | --- |
| Framework | ESX Legacy, QBCore, Qbox, ND Framework, ox\_core, standalone | `Framework` |
| Inventory | ox\_inventory, qs-inventory, codem-inventory, core\_inventory, tgiann-inventory, origen\_inventory, qb-inventory, ps-inventory, lj-inventory, framework items | `Inventory` |
| Target | ox\_target, qb-target, none (text UI prompts) | `Target` |
| Notifications | ox\_lib, okokNotify, brutal\_notify, wasabi\_notify, lation\_ui, codem-notification, mythic\_notify, pNotify, t-notify, k5\_notify, vms\_notify, Qbox, QBCore, ESX, GTA, chat, custom | `Notify.system` |
| Progress bar | ox\_lib (bar or circle), lation\_ui, esx\_progressbar, QBCore progressbar, mythic\_progbar, rprogress, progressBars, none, custom | `Progress.system` |
| Text UI | ox\_lib, okokTextUI, jg-textui, cd\_drawtextui, brutal\_textui, lation\_ui, QBCore, ESX, GTA, custom | `TextUI.system` |
| Menus and dialogs | ox\_lib, lation\_ui | `Menu.system` |
| Job money | lvl\_banking, okokBanking, Renewed-Banking, qb-banking, qb-management, esx\_addonaccount | `Society` |

## Requirements

* OneSync
* [ox\_lib](https://github.com/overextended/ox_lib/releases/latest)
* [oxmysql](https://github.com/overextended/oxmysql/releases/latest) (only for scripts that save data)

## Installation

1. Put `lvl_core` into your resources folder.
2. Add it to `server.cfg` **after** your framework, inventory, target and UI resources and **before** every lvl script:

```
ensure ox_lib
ensure es_extended      # or qb-core / qbx_core / ND_Core / ox_core
ensure ox_inventory     # your inventory
ensure ox_target        # your target
ensure lvl_core
ensure lvl_dealership   # your lvl scripts
```

3. Start the server and check the console (see below).
4. Optional: give admins the ACE permission that works on every framework:

```
add_ace group.admin lvl.admin allow
```

## Auto detection

Everything is set to `'auto'` by default. On start lvl\_core looks at what is running and prints one line:

```
[lvl_core] Framework: esx | Inventory: ox_inventory | Notify: ox_lib | Progress: ox_lib | Text UI: ox_lib | Target: ox_target
```

| Message | Meaning | What to do |
| --- | --- | --- |
| **WARNING** | More than one was found (for example two inventories). lvl\_core uses the first one. | Set the value the warning shows in `config.lua`. |
| **ERROR** | The value in `config.lua` is not running or is not supported. lvl\_core falls back to auto. | Fix the value or start the resource. |
| **WARNING** resource started after lvl\_core | A framework or inventory started later than lvl\_core. | Move `ensure lvl_core` lower in `server.cfg`. |

`/lvlcore` (server console or an admin in game) prints the detection again.

## Configuration

### config.lua

```lua
ServerName = 'Level RP',   -- notification title when a script has none

Locale = 'en',             -- language of ALL lvl scripts: 'en' or 'cs' (nil = from ox_lib)

Debug = false,             -- debug prints of all lvl scripts
```

#### Bridge

```lua
-- 'auto' | 'esx' | 'qb' | 'qbx' | 'nd' | 'ox' | 'standalone'
Framework = 'auto',

-- 'auto' | 'ox_inventory' | 'qs-inventory' | 'codem-inventory' | 'core_inventory'
-- | 'tgiann-inventory' | 'origen_inventory' | 'qb-inventory' | 'ps-inventory'
-- | 'lj-inventory' | 'framework'
Inventory = 'auto',

-- 'auto' | 'ox_target' | 'qb-target' | 'none'
-- none = no target, scripts show text UI prompts instead
Target = 'auto',

-- 'auto' | 'lation_ui' | 'ox_lib'
-- switches notifications, progress bar, text UI and menus at once
UI = 'auto',

-- job money: 'auto' | 'lvl_banking' | 'okokBanking' | 'Renewed-Banking'
-- | 'qb-banking' | 'qb-management' | 'esx_addonaccount' | 'none'
Society = 'auto',
```

A single setting below wins over `UI`. For example `UI = 'lation_ui'` with `Notify.system = 'okokNotify'` uses Lation for everything except notifications.

#### Notifications

```lua
Notify = {
    system = 'auto',      -- see the table above, 'custom' = your own function
    duration = 6000,      -- ms
    position = nil,       -- ox_lib only, nil = top right

    -- custom = function(data)
    --     exports.my_notify:Show(data.title, data.description, data.type, data.duration)
    -- end,
    -- data = { title, description, type ('success'|'error'|'warning'|'inform'), duration, icon }
},
```

#### Progress bar

```lua
Progress = {
    system = 'auto',      -- 'none' = no bar, only the wait and the animation
    style = 'bar',        -- ox_lib only: 'bar' or 'circle'
    disable = { car = true, move = true, combat = true },
    useWhileDead = false,

    -- custom = function(data) return exports.my_progress:Start(data.label, data.duration) end,
    -- data = { label, duration, canCancel, disable, anim = { dict, clip, flag }, prop }
    -- must return true (finished) or false (cancelled)
},
```

Animation, prop, disabled controls and cancel (X) work with every progress system, also with the ones that do not support them on their own.

#### Text UI and menus

```lua
TextUI = {
    system = 'auto',
    -- custom = {
    --     show = function(text, opts) exports.my_textui:Show(text) end,
    --     hide = function() exports.my_textui:Hide() end,
    -- },
},

Menu = {
    system = 'auto',      -- 'auto' = lation_ui if it is running, else ox_lib
},
```

#### Units, money and jobs

```lua
Units = 'metric',     -- 'metric' (km/h, m) or 'imperial' (mph, ft)
Currency = { symbol = '$', before = true, separator = ' ' },   -- "$12 500"

PoliceJobs = { 'police', 'sheriff' },
EmergencyJobs = { 'police', 'sheriff', 'ambulance', 'lsfd', 'sahp', 'doj' },

-- groups that count as admin (ESX group, QBCore permission), ACE lvl.admin works too
AdminGroups = { admin = true, superadmin = true, owner = true, god = true },

Font = nil,           -- font name for blip labels, must be registered by another resource
ClosestPlayer = { distance = 4.0, marker = { r = 74, g = 159, b = 224, a = 160 } },
```

### server/config.lua

Only the server reads this file, players cannot download it.

```lua
-- named Discord webhooks, scripts use them by key: Config.Webhook = 'motel'
ServerConfig.Webhooks = {
    default = '',     -- used when a key is missing, empty = no log
    -- motel = 'https://discord.com/api/webhooks/...',
    -- dealership = 'https://discord.com/api/webhooks/...',
}

ServerConfig.DefaultColor = 0x2B7AC0   -- embed colour
ServerConfig.RateLimit = 25            -- max messages per webhook per minute
ServerConfig.VersionCheck = true       -- check for new versions on start
ServerConfig.JobCountCache = 10        -- seconds between job count updates
```

{% hint style="info" %}
Keep webhook URLs here, never in a `config.lua`. Players can download every `config.lua` that is a shared script.
{% endhint %}

## Commands

| Command | Who | What it does |
| --- | --- | --- |
| `/lvlcore` | server console, admins | Prints what lvl\_core detected |

## For developers

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

### Exports

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
