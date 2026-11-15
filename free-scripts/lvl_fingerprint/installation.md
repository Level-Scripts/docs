# Installation

1. Put `lvl_fingerprint` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_fingerprint
```

3. Pick how officers open the scanner in `Config.InteractMethod`.
4. Put your department logos into `html/img/` and set them in `Config.LawEnforcements`.
5. For `InteractMethod = 'item'`, add the item to your inventory:

```lua
['fingerprint'] = {
    label = 'Fingerprint Scanner',
    weight = 300,
    stack = false,
    close = true,
},
```
