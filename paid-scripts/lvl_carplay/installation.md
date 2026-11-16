# Installation

## Installation

1. Put `lvl_carplay` into your resources.
2. Add it to `server.cfg` after xsound and lvl\_core:

```
ensure xsound
ensure lvl_core
ensure lvl_carplay
```

3. Optional: add search keys to `Config.Keys` (see [Search keys](configuration.md#search-keys)).
4. Restart. No database and no items, playlists and places are saved in the server KVP.

{% hint style="warning" %}
If another script turns the vehicle radio off (`SetVehRadioStation` to off or `SetUserRadioControlEnabled(false)`), the GTA stations stay silent.
{% endhint %}
