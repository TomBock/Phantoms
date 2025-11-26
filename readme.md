# Phoenix Phantoms
A Paper plugin that makes Phantoms progressively stronger the longer a player stays awake.
The plugin introduces custom upgrades, configurable loot, a shop system, and placeholders for other plugins.


## Features
- Phantoms get stronger the longer players stay awake, starting from a configurable day (e.g. day 9)
- Fully configurable upgrades tiers (speed, health, damage, size, effects, loot)
- Customizable loot system based on tiers
- **Optional** shop commands to sell collected items for rewards
- Placeholder support for displaying awake time and sold items

## Requirements
- PaperMC 1.20.x or 1.21.x
- Java 21
- [Vault](https://www.spigotmc.org/resources/vault.34315/)
- [LuckPerms](https://www.spigotmc.org/resources/luckperms.28140/)
- (Optional) [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/)


## Commands
| Command                    | Description                                                                             |
|----------------------------|-----------------------------------------------------------------------------------------|
| `/awake <days>`            | Sets the number of days without sleep for yourself                                      |
| `/phantom <item> <player>` | Attempts to sell a shop item to a player (execute as NPC). The items come from shop.yml |
| `/phantom resetlimit`      | Resets the previously sold items (not titles) for all players                           |

## Permissions
| Permission                    | Description                             |
|-------------------------------|-----------------------------------------|
| `phoenixphantoms.admin`       | Grants access to all admin commands     |


## Placeholders
| Placeholder                       | Description                                                |
|-----------------------------------|------------------------------------------------------------|
| `%phoenixphantom_{item}%`         | Amount of items sold: `0/25`                               |
| `%phoenixphantom_awake%`          | Amount of days without sleep: `3.14`                       |
| `%phoenixphantom_awake_{player}%` | Amount of days without sleep for a specific player: `3.14` |

## Configs

- `config.yml` - Phantom upgrades, spawn rules & loot
- `msg.yml` - Player facing messages
- `shop.yml` - Shop items, limits, prices & rewards
- `sold_items.yml` - Tracks sold items per player

Config.yml
```yaml
spawn_start: 9 # At how many sleepless minecraft days Phantoms start spawning
debug: false # Whether debug messages should be printed to console
placeholder:
  sold_items_color: "§6§l"

upgrades:
  1: # Active after 1 day over the spawn_start
    # All properties are optional
    name: "Small Phantom"
    speed: 1
    health: 9
  2: # After 2 days over...
  5: # After 3 days over...
    name: "Large Phantom"
    speed: 2
    health: 20
    damage: 15
    knockback: 2
    size: 3
    effects:
      fire_resistance: 1 # Potion effect level
      #...
    loot:
      - default # Allows vanilla loot
      - phantom_skin:0.1 # 10% chance to drop phantom_skin

# All loot types must be defined here (except 'default')
loot:
  phantom_skin:
    ==: org.bukkit.inventory.ItemStack
    v: 4189
    type: FEATHER
    amount: 1
    meta:
      ==: ItemMeta
      meta-type: UNSPECIFIC
      display-name: '{"text":"Phantom Skin","color":"yellow"}'
      lore:
        - '{"text":"_","color":"gray"}'
```
