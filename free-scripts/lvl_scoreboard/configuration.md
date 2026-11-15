# Configuration

## config.lua

```lua
Config.Framework = 'auto'         -- 'auto' | 'esx' | 'qb' | 'qbx'

Config.PressKey = 'DELETE'        -- default key
Config.CommandName = 'scoreboard'

Config.Side = 'right'             -- 'left' or 'right'

Config.UseDiscordAvatar = true
Config.UseDiscordName = true

Config.ServerName = 'Level RP'
Config.MaxPlayers = nil           -- nil = from sv_maxclients

Config.RefreshInterval = 2000     -- ms, refresh while open

Config.UseGameTime = false        -- true = in-game time, false = real time
Config.TimeFormat = {
    timeFormat = '24h',           -- '24h' or '12h'
    plusHours = 1,                -- time zone offset, can be negative
}

Config.ShowPlayerId = true
Config.ShowJob = true
Config.ShowPing = true
Config.PingThresholds = { good = 80, mid = 150 }   -- green up to good, orange up to mid, red above
```

## Jobs

```lua
Config.ShowJobs = true
Config.JobsToShow = {
    -- name = framework job, label = text (from the framework when missing), icon = Font Awesome
    { name = 'police',    label = locale('police'),   icon = 'fa-solid fa-shield-halved' },
    { name = 'ambulance', label = 'EMS',              icon = 'fa-solid fa-truck-medical' },
    { name = 'mechanic',  label = locale('mechanic'), icon = 'fa-solid fa-wrench' },
    { name = 'lawyer',    label = locale('lawyer'),   icon = 'fa-solid fa-scale-balanced' },
    { name = 'taxi',      label = locale('taxi'),     icon = 'fa-solid fa-taxi' },
}
```

## Illegal activities

```lua
Config.ShowIllegalActivities = true
Config.PoliceJobs = { 'police', 'sheriff' }
Config.PoliceOnDuty = true       -- QBCore and Qbox: count only police on duty
Config.IllegalActivities = {
    { name = locale('bank_robbery'),   minPolice = 3, icon = 'fa-solid fa-piggy-bank' },
    { name = locale('house_burglary'), minPolice = 2, icon = 'fa-solid fa-house' },
    { name = locale('store_robbery'),  minPolice = 1, icon = 'fa-solid fa-shop' },
    { name = locale('drug_sale'),      minPolice = 2, icon = 'fa-solid fa-pills' },
    { name = locale('car_theft'),      minPolice = 2, icon = 'fa-solid fa-car' },
}
```

Players only see available or not available, never the number of officers.

## Discord role icons

```lua
Config.DiscordRoles = {
    {
        label = 'Owner',             -- tooltip
        roleId = '000000000000000000',  -- Discord role ID
        icon = 'fa-solid fa-crown',  -- Font Awesome icon
        color = '#4A9FE0',
    },
}
```

Right click a role in Discord (with Developer Mode on) and **Copy Role ID**.

## config\_server.lua

Server only, players never download this file.

```lua
ServerConfig.BotToken = GetConvar('lvl_scoreboard_token', '')   -- the convar wins
ServerConfig.GuildId = ''               -- your Discord server ID
ServerConfig.DiscordCacheTime = 1800    -- seconds before Discord data is loaded again
```
