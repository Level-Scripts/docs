# Installation

1. Put `lvl_illegalusb` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_illegalusb
```

3. Add the items. ox\_inventory `data/items.lua` (also in `INSTALL/ox_items.txt`):

```lua
['usb_lockpick'] = { label = 'Lockpick', weight = 160 },

['usb_blue']   = { label = 'USB Blue',   weight = 10, stack = true, close = true },
['usb_green']  = { label = 'USB Green',  weight = 10, stack = true, close = true },
['usb_pink']   = { label = 'USB Pink',   weight = 10, stack = true, close = true },
['usb_purple'] = { label = 'USB Purple', weight = 10, stack = true, close = true },
['usb_red']    = { label = 'USB Red',    weight = 10, stack = true, close = true },
['usb_yellow'] = { label = 'USB Yellow', weight = 10, stack = true, close = true },
```

A QBCore version is in `INSTALL/qb_items.txt`.

4. Connect your hacking minigame (`client/editable.lua`), lockpick minigame and dispatch (`config.lua`).
5. Put the USBs into your shops, loot tables or crafting.
