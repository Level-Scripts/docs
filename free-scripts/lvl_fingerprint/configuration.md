# Configuration

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

## BOLO

Return `true`, `false` or a short text. Connect your MDT here (server side):

```lua
Config.GetBoloStatus = function(identifier)
    -- return exports.my_mdt:HasBolo(identifier)
    return false
end
```
