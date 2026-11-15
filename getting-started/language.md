---
description: Change the language of all Level Scripts at once, or edit any text.
---

# Language

## Pick the language

The language is set **once** for all Level Scripts in `lvl_core/config.lua`:

```lua
Locale = 'en',   -- 'en' = English, 'cs' = Czech
```

* `nil` takes the language from ox\_lib (`setr ox:locale "en"` in `server.cfg`).
* A text that is missing in the chosen language falls back to English.

Restart the scripts after you change it.

{% hint style="info" %}
You never set the language in the config of a single script. Every lvl script reads it from lvl\_core.
{% endhint %}

## Edit texts

Every script has a `locales` folder:

```
lvl_motel/
└─ locales/
   ├─ en.json
   └─ cs.json
```

Open the file of your language and change the text after the colon. Keep the key (left side) as it is.

```json
"rent_room": "You rented the room for %s.",
```

`%s` and `%d` are filled in by the script (a name, a price, a number). Keep them in the text.

## Add a new language

1. Copy `en.json` to a new file, for example `de.json`.
2. Translate the texts.
3. Set `Locale = 'de'` in `lvl_core/config.lua`.

Do this for every script you use. Texts you do not translate stay in English. If you made a full translation, share it on our [Discord](https://www.discord.gg/UKqwhpjczw) and we add it to the next update.
