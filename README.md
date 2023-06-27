# BlockReplacer

[![](https://poggit.pmmp.io/shield.state/BlockReplacer)](https://poggit.pmmp.io/p/BlockReplacer)
[![](https://poggit.pmmp.io/shield.dl.total/BlockReplacer)](https://poggit.pmmp.io/p/BlockReplacer)

A PocketMine-MP plugin that replaces a block with another block at a predetermined time.

# Features

- **Automatic Update Checker**: The plugin automatically checks for updates, ensuring that you have the latest version with new features and bug fixes.
- **Permission Bypass**: Grant specific users the `blockreplacer.bypass` permission to allow them to bypass block replacement and interact with blocks without triggering the replacement process.
- **Automatic Item Pickup Support**: Enable automatic pickup of items dropped after block replacement, making it convenient for players to collect them.
- **Custom Block Replacement**: Define rules for replacing specific blocks, allowing you to create unique environmental transformations and dynamic gameplay scenarios.
- **Custom Drop Block**: Specify custom blocks to be dropped when certain blocks are broken, adding variety and alternative interactions. You can even include custom drop experience blocks, providing players with experience orbs upon block destruction.
- **World Blacklist and Whitelist Support**: Control block replacement in specific worlds using blacklists and whitelists, providing tailored gameplay experiences.
- **Sound Customization Support**: Customize the sounds associated with block replacement, enhancing immersion and creating a unique audio experience.
- **Particle Customization Support**: Customize particle effects during block replacement, adding visual flair and enhancing the overall aesthetic appeal.
- **Block Replacement during Server Stop**: Block replacement continues when the server is stopped, and changes are applied upon server restart.
- **Scheduled Block Replacement**: Schedule block replacement at specific times or intervals, automating changes to the game environment.

# Permissions

- `blockreplacer.bypass`: Grants users the ability to bypass block replacement, allowing them to interact with blocks without triggering the replacement process.

# Default Config
```yaml
# BlockReplacer Configuration

# Permission defaults for the "blockreplacer.bypass" permission.
# This permission allows players to bypass block replacement.
# Valid values:
#   - op: All server operators (ops) are assigned this permission by default.
#   - all: Everyone is assigned this permission by default.
#   - none: No one is assigned this permission by default.
permission:
  defaults: op

# Automatic Item Pickup
# Dropped items will be automatically added to the player's inventory.
# If the player's inventory is full, the item will be dropped near the player.
# This also includes experience points.
auto-pickup:
  enabled: true

# Block Replacement Rules
blocks:
  # The default block used for replacement.
  default-replace: air
  # The default time (in seconds) before a block is replaced with the previous block.
  default-time: 60
  # List of block replacement rules.
  # This should also always be wrapped in quotes to ensure it is parsed correctly.
  # Format: "block_from=block_to=time".
  # If "block_to" is not set, it will be replaced with the default replacement block.
  # If "time" is not set, it will be replaced with the default replacement time.
  list:
    # Example 1: Replace cobblestone with stone within 5 seconds, with drops and experience.
    "cobblestone=stone=5":
      drops:
        - item: stone
          amount: 1-2  # Amount range: from 1 to 2
          chance: 50-100  # Chance range: from 50% to 100%
      experience:
        amount: 5  # Fixed experience amount
        chance: 100  # Fixed chance

    # Example 2: Replace oak log with spruce log within 10 seconds, no drops, and double experience.
    "oak_log=spruce_log=10":
      drops: []
      experience:
        amount: 2  # Double the default experience amount
        chance: 100  # Fixed chance

    # Example 3: Replace diamond ore with emerald ore, follows default replacement time, with drops and experience.
    "diamond_ore=emerald_ore":
      drops:
        - item: emerald
          amount: 1-2  # Amount range: from 1 to 2
          chance: 50-100  # Chance range: from 50% to 100%
      experience:
        amount: 10  # Fixed experience amount
        chance: 50  # Fixed chance

    # Example 4: Replace redstone ore with glowstone, within 8 seconds, with drops and quadruple experience.
    "redstone_ore=glowstone=8":
      drops:
        - item: glowstone_dust
          amount: 4-6  # Amount range: from 4 to 6
          chance: 80-100  # Chance range: from 80% to 100%
      experience:
        amount: 4  # Quadruple the default experience amount
        chance: 100  # Fixed chance

    # Example 5: Replace oak wood with acacia wood within 15 seconds, no drops, and custom experience.
    "oak_wood=acacia_wood=15":
     drops: []
     experience:
       amount: 10  # Fixed experience amount
       chance: 100  # Fixed chance

    # Example 6: Replace stone with random wool color, follows default replacement time, with drops and experience.
    "stone":
      drops:
        - item: wool
          amount: 1-3  # Amount range: from 1 to 3
          chance: 50-100  # Chance range: from 50% to 100%
      experience:
        amount: 5  # Fixed experience amount
        chance: 100  # Fixed chance

    # Example 7: Replace gold ore with default replacement block and time, with drops and a unique item tool.
    "gold_ore":
      drops:
        - item: diamond_pickaxe
          amount: 1  # Fixed amount
          chance: 10  # Fixed chance
          name: "§6Efficiency's Edge"  # Custom name for the item
          lore:
            - "§eHarness the power of swiftness." # Custom lore for the item
            - "§bWithstands the test of time and labor."
            - "§aEffortlessly carves through any material."
          enchantments:
            - name: haste
              level: 3
            - name: efficiency
              level: 5
            - name: unbreaking
              level: 3

# Particle Effects
particles:
  # Whether to display particles when destroying blocks.
  enabled: true
  # The name of the particle to be displayed when destroying the previous block.
  from: minecraft:villager_happy
  # The name of the particle to be displayed when replacing the block after it.
  to: minecraft:explosion_particle

# Sound Effects
sounds:
  # Whether to play sound effects when destroying blocks.
  enabled: true
  # The volume of the sound effects.
  volume: 1
  # The pitch of the sound effects.
  pitch: 1
  # The name of the sound to be played when destroying the previous block.
  from: random.orb
  # The name of the sound to be played when replacing the block after it.
  to: random.explode

# World Configuration
worlds:
  # Set this to true if you want to use the blacklisted-worlds setting.
  # If both enabled-world-blacklist and enabled-world-whitelist are set to the same setting,
  # the block will be replaced for all worlds.
  enabled-world-blacklist: false
  # If enabled-world-blacklist is set to true, the block will be replaced for all worlds,
  # except the worlds mentioned here.
  blacklisted-worlds:
    - blacklistedworld1
    - blacklistedworld2
  # Set this to true if you want to use the whitelisted-worlds setting.
  # If both enabled-world-blacklist and enabled-world-whitelist are set to the same setting,
  # the block will not be replaced for all worlds.
  enabled-world-whitelist: false
  # If enabled-world-whitelist is set to true, blocks will not be replaced for all worlds,
  # except the worlds mentioned here.
  whitelisted-worlds:
    - whitelistedworld1
    - whitelistedworld2

```

# Upcoming Features

- Currently none planned. You can contribute or suggest for new features.

# Additional Notes

- If you find bugs or want to give suggestions, please visit [here](https://github.com/AIPTU/BlockReplacer/issues).
- We accept all contributions! If you want to contribute, please make a pull request in [here](https://github.com/AIPTU/BlockReplacer/pulls).
- Icons made from [www.flaticon.com](https://www.flaticon.com)
