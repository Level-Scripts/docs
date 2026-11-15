# Configuration

```lua
-- inventory size without a bag
Config.DefaultInventory = {
    slots = 50,
    weight = 24000,   -- grams
}

-- slots and weight ADDED to DefaultInventory while the piece is worn
Config.ClothesBackpacks = {
    { component = 5, drawable = 40, slots = 10, weight = 8000 },
    { component = 5, drawable = 41, slots = 10, weight = 8000 },
    { component = 5, drawable = 44, slots = 12, weight = 10000 },
    { component = 5, drawable = 45, slots = 12, weight = 10000 },
    { component = 5, drawable = 81, slots = 14, weight = 12000 },
    { component = 5, drawable = 82, slots = 14, weight = 12000 },
    { component = 5, drawable = 85, slots = 15, weight = 15000 },
    { component = 5, drawable = 86, slots = 15, weight = 15000 },
    { component = 4, drawable = 102, slots = 4, weight = 2000 },
}
```

| Field | Meaning |
| --- | --- |
| `component` | Clothing slot: `5` = bags, `4` = legs, `11` = torso... |
| `drawable` | Number of the clothing piece in that slot |
| `slots` | Slots added |
| `weight` | Grams added |

{% hint style="info" %}
Set `DefaultInventory` to the same size your inventory uses for players (for ox\_inventory `inventory:slots` and `inventory:weight`), otherwise players without a bag get a different size.
{% endhint %}

## Find the drawable number

Open your clothing menu, go to **Bags** and pick the bag. The number shown next to it is the `drawable`. Pants pockets or vests work the same way with their own `component`.
