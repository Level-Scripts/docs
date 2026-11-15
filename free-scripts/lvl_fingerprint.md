---
description: >-
  Police fingerprint scanner. The officer scans a player and sees name, date
  of birth, gender and BOLO status on a handheld device.
---

# lvl\_fingerprint

[Get it on Tebex](https://level-scripts.tebex.io/package/7364003) | [Discord](https://www.discord.gg/UKqwhpjczw)

An officer opens the scanner on a handheld device and requests a scan from the player in front of them. The player has to hold their finger on the scanner on their own screen, they can also refuse. When the scan finishes the officer sees the identity of the player. Every department gets its own logo and colour.

## Features

* **Two sided scan**: the scanned player holds the button to give the fingerprint, or cancels
* **Identity result**: first name, last name, date of birth, gender, BOLO, citizen ID (each one can be hidden)
* **BOLO hook** for your MDT
* **Scan history** on the device
* **Department look**: logo and colour per job
* Open with **target**, an **item** or a **command**
* Animations with a handheld prop
* Job and distance are checked on the server
* English and Czech, every text editable

## Requirements

| Resource | |
| --- | --- |
| [lvl\_core](../lvl_core.md) | required |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required |
| ox\_target or qb-target | only for `InteractMethod = 'target'` |
| Framework | any supported by lvl\_core |

## Installation

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

## How to use

| Method | How |
| --- | --- |
| `target` | Target a player, **Scan** |
| `item` | Use the scanner item in front of a player |
| `command` | Type `/fingerprint` in front of a player |

The scanned player sees the scanner and holds the button until the scan is done. The officer then sees the result and it is saved in the history.

## Configuration

```lua
Config.InteractMethod = 'target'    -- 'target', 'item' or 'command'
Config.ItemName = 'fingerprint'     -- for 'item'
Config.CommandName = 'fingerprint'  -- for 'command'

-- jobs that can scan, logo = image in html/ (empty = shield icon in the job colour)
Config.LawEnforcements = {
    ['police'] = {
        logo = 'img/lspd.png',
        color = '#2651c9',
    },
    ['sheriff'] = {
        logo = 'img/lssd.png',
        color = '#ccbe00',
    },
}

-- animation while the app is open
Config.HoldAnim_Dict = 'cellphone@'
Config.HoldAnim = 'cellphone_text_read_base'

-- animation while scanning
Config.ScanAnim_Dict = 'random@hitch_lift'
Config.ScanAnim = 'idle_f'

-- fields shown in the result
Config.DisplayFields = {
    firstname = true,
    lastname = true,
    dob = true,
    gender = true,
    bolo = true,
    citizenid = false,
}
```

### BOLO

Return `true`, `false` or a short text. Connect your MDT here (server side):

```lua
Config.GetBoloStatus = function(identifier)
    -- return exports.my_mdt:HasBolo(identifier)
    return false
end
```

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>You do not have permission to use fingerprint scanner</summary>

The job of the officer must be a key in `Config.LawEnforcements`.

</details>

<details>

<summary>The logo is missing</summary>

The image must be inside the `html` folder of the script (for example `html/img/lspd.png`) and `logo` is the path from `html/`, here `img/lspd.png`.

</details>
