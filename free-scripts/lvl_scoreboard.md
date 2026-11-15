---
description: >-
  Player list with Discord avatars, names and role icons, job counts, ping and
  illegal activity availability by police count.
icon: clipboard
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: hero
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# lvl\_scoreboard

[Get it on Tebex](https://level-scripts.tebex.io/package/scoreboard) | [Discord](https://www.discord.gg/UKqwhpjczw)

A clean scoreboard on the side of the screen. It shows every player with their Discord avatar, name and role icons, the number of players in each job and which illegal activities are available right now based on the police online. Players search the list by name or ID.

## Features

* **Player list** with ID, job and ping
* **Discord avatars, names and role icons** through a bot
* **Job counts** with icons
* **Illegal activities** with the police needed, police count itself is never sent to players
* **Search** by name or ID
* **Server time** or in-game time, 24h or 12h
* Left or right side of the screen
* **Lightweight**: one shared snapshot for all players, Discord data loaded once per player and cached
* Bot token stays on the server, players cannot download it
* English and Czech, every text editable

## Requirements

| Resource                                                          |                        |
| ----------------------------------------------------------------- | ---------------------- |
| [lvl\_core](../lvl_core.md)                                       | required               |
| [ox\_lib](https://github.com/overextended/ox_lib/releases/latest) | required               |
| ESX, QBCore, Qbox or standalone                                   | detected automatically |

## Installation

1. Put `lvl_scoreboard` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_scoreboard
```

3. Optional, for Discord avatars, names and role icons:
   1. Create a bot in the [Discord Developer Portal](https://discord.com/developers/applications) and turn on **Server Members Intent**.
   2. Invite the bot to your Discord server.
   3. Add the token to `server.cfg`:

```
set lvl_scoreboard_token "YOUR_BOT_TOKEN"
```

4. Put your Discord server (guild) ID into `config_server.lua`.

{% hint style="danger" %}
Never put the bot token into `config.lua`. Players download that file. Use the convar or `config_server.lua`.
{% endhint %}

## Commands and controls

| Command / key | What it does                                                                       |
| ------------- | ---------------------------------------------------------------------------------- |
| `DELETE`      | Opens and closes the scoreboard. Players can change the key in FiveM key bindings. |
| `/scoreboard` | Same as the key                                                                    |

## Configuration

### config.lua

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

### Jobs

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

### Illegal activities

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

### Discord role icons

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

### config\_server.lua

Server only, players never download this file.

```lua
ServerConfig.BotToken = GetConvar('lvl_scoreboard_token', '')   -- the convar wins
ServerConfig.GuildId = ''               -- your Discord server ID
ServerConfig.DiscordCacheTime = 1800    -- seconds before Discord data is loaded again
```

## Language

The language comes from [lvl\_core](../lvl_core.md). Texts are in `locales/en.json` and `locales/cs.json`, see [Language](../getting-started/language.md).

## FAQ

<details>

<summary>No Discord avatars or names</summary>

Check that the token is set, the bot is on your Discord server, **Server Members Intent** is on and `GuildId` is right. The player also needs Discord running when joining FiveM.

</details>

<details>

<summary>A job shows 0 players</summary>

`name` in `Config.JobsToShow` must be the exact job name of your framework (for example `ambulance`, not `ems`).

</details>
