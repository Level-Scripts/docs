# Configuration

All options are in `config.lua`.

## General

```lua
Config.Command = 'carplay'
Config.Key = 'F7'

Config.PassengersCanDrive = false   -- passengers can use autopilot and cruise control
```

## Music

```lua
Config.Radio = {
    DefaultVolume = 35,
    MaxQueue = 50,
    SpotifyPlaylistLimit = 30,
    SearchResults = 12,
    BlacklistedClasses = { 13, 21 },
    BlacklistedModels = {},

    OutsideHearing = true,   -- music is heard outside the car
    OutsideRange = 14.0,
    OutsideVolume = 0.45,    -- closed car
    OpenVolume = 0.85,       -- open doors, windows or roof
    InCarVolume = 0.25,      -- music from another car heard inside yours
    FadeSpeed = 120,
    NotifyTrackChange = true,
}
```

## Search keys

Optional, server side only.

```lua
Config.Keys = {
    YouTubeApiKey = '',        -- console.cloud.google.com
    SpotifyClientId = '',      -- developer.spotify.com, for Spotify search
    SpotifyClientSecret = '',
}
```

## Autopilot

```lua
Config.Autopilot = {
    Mode = 'models',   -- 'all' | 'none' | 'models'
    Models = { 'raiden', 'raidenz', 'neon', 'cyclone', 'cyclone2', 'cycloneex0', 'imorgon', 'iwagen',
               'omnisegt', 'virtue', 'voltic', 'tezeract', 'khamelion', 'dilettante', 'surge', 'comet7' },
    BlacklistedClasses = { 8, 13, 14, 15, 16, 21 },

    SpeedLimits = {   -- km/h
        City = 50,
        Rural = 90,
        Highway = 130,
        HighwayStreets = { 'Los Santos Freeway', 'Del Perro Fwy', 'Olympic Fwy', 'La Puerta Fwy',
                           'Elysian Fields Fwy', 'Palomino Fwy', 'Senora Fwy', 'Great Ocean Hwy' },
        Streets = {},   -- own limit per street, e.g. ['Vespucci Blvd'] = 40
    },

    StopDistance = 20.0,
    DrivingStyle = 786603,          -- follows traffic rules
    TakeOverCancels = true,
    RemoveWaypointOnArrival = true,
}
```

## Cruise control

```lua
Config.Cruise = {
    Enabled = true,
    MinSpeed = 30,
    MaxSpeed = 200,
    Step = 5,
    Presets = { 30, 50, 80, 90, 130 },
    BrakeCancels = true,
}
```

## Vehicle

```lua
Config.Roof = { Enabled = true, MaxSpeed = 40, PassengersCanUse = true }

Config.Vehicle = {
    Enabled = true,
    PassengersCanUse = false,
    OwnWindow = true,       -- passengers can roll their own window
    Lock = true,            -- false if you use a keys script
    Engine = false,
    MaxSpeedDoors = 15,
}
```

## Map and places

```lua
Config.Map = {
    Style = 'atlas',        -- 'satellite' | 'atlas', own maps with tools/maptiles.py
    ShareWaypoint = true,   -- destination shared with passengers
}

Config.Places = {
    Max = 20,
    Nearest = { { label, icon, sprite [, colour] }, ... },   -- found by the map blip sprite
    Icons = { ... },
}

Config.Playlists = { Max = 20, MaxItems = 100 }
```

## Radio stations

```lua
Config.Stations = {
    List = {
        { id = 'RADIO_02_POP', label = 'Non-Stop-Pop FM', desc = '...', icon = 'star' },
        ...
    },
}
```

The order is the menu order. Stations missing in your game build are hidden.

## Other

```lua
Config.Audio = { XSoundResource = 'xsound', LoadTimeout = 20 }
Config.Streamer = { VolumeCommand = 'carvolume' }
```

## Exports

Client exports:

* `exports.lvl_carplay:isCruiseActive()`: Is cruise control on
* `exports.lvl_carplay:getStreamerMode()`: Is streamer mode on
* `exports.lvl_carplay:setStreamerMode(state)`: Turns streamer mode on or off
* `exports.lvl_carplay:getPersonalVolume()`: Personal car music volume
* `exports.lvl_carplay:setPersonalVolume(volume)`: Sets the personal car music volume

Client event `lvl_carplay:cruise` fires when cruise control turns on or off (for HUDs).
