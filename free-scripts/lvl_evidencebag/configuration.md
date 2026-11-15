# Configuration

```lua
Config.Policejobs = { 'police', 'sheriff' }   -- jobs that can use evidence bags

Config.EBItems = {
    full = 'evidence_bag_full',
    empty = 'evidence_bag_empty',
}

Config.EBLabelPrefix = 'EB - '   -- start of every bag label

Config.MaxDistance = 3.0         -- metres between officer and player

Config.Stash = { slots = 50, weight = 50000 }   -- size of one bag (grams)

-- items that stay with the player
Config.ProhibitedItems = {
    'water',
    'sandwich',
    'burger',
    'cola',
    'apple',
}
```
