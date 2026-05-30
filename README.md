# CrownandBanner
the makings of a mod
## Commands

### General

- `/cab info`
  - Shows a short help message.

### Factions

- `/cab faction list`
  - Lists registered factions.

- `/cab faction info <id>`
  - Shows faction power, territory count, and hostile relations.
  - Starter faction ids: `villagers`, `pillagers`, `player`.

### Territory

- `/cab territory info`
  - Shows the current region owner, contesting faction, capture/control progress, linked settlement, and occupation state.

- `/cab territory claim <faction>`
  - Claims the current territory region for a faction.

- `/cab territory release`
  - Releases the current territory region back to wilderness.

- `/cab territory contest <faction>`
  - Marks the current region as contested by a faction.

- `/cab territory advance`
  - Advances capture progress for the current contested region by the configured capture step.

### Recruiting

- `/cab recruit`
  - Recruits the villager the player is looking at, if valid.

### Squads

- `/cab squad create`
  - Creates an active squad from nearby recruited villagers.

- `/cab squad info`
  - Shows active squad command, formation, and member count.

- `/cab squad follow`
  - Orders the active squad to follow the player.

- `/cab squad hold`
  - Orders the active squad to hold the player’s current position.

- `/cab squad patrol`
  - Orders the active squad to patrol around the player’s current position.

- `/cab squad defend`
  - Orders the active squad to defend the player’s current position and attack nearby hostiles.

- `/cab squad attack`
  - Orders the squad to attack the nearest hostile mob nearby.

- `/cab squad assault`
  - Uses the active squad to contest the current non-player territory for the player.
  - Wilderness regions are claimed directly.

- `/cab squad retreat`
  - Orders the active squad to retreat toward the player.

- `/cab squad formation <type>`
  - Changes squad formation.
  - Valid values: `line`, `column`, `ring`.
## Gameplay Mechanics

### Territory

- The world is divided into persistent territory regions.
- Regions can be wilderness, owned, or contested.
- Capture is gradual: contested regions have control progress from `10000` down to `0`.
- When capture reaches `0`, the contesting faction takes ownership.
- Defenders can now stabilize a region by winning battle ticks, restoring control back toward `10000`.

### Banner Claiming

- Placing a banner in wilderness claims the region for the `player` faction.
- Placing a banner in hostile territory contests that region for the player and starts a conflict.
- Neutral territory cannot be claimed by banner.

### Factions

- Starter factions are `villagers`, `pillagers`, and `player`.
- Pillagers are hostile to villagers and the player by default.
- Factions track territory count, power, color, and hostile relations.

### Settlements

- Villages and pillager outposts are detected from world structures.
- Detected villages become villager settlements.
- Detected pillager outposts become pillager settlements.
- Settlements claim nearby territory automatically.
- Settlements store tier, population, food, security, morale, damage, and occupation state.

### Strategic Simulation

- Pillagers periodically evaluate nearby villager border regions.
- Pillagers can start conflicts without the player being nearby.
- If a player is far away, conflicts resolve statistically.
- If a player is nearby, conflicts use physical battle logic and can spawn limited pillager reinforcements.

### Capture And Occupation

- When a settlement region is captured by an enemy faction, the settlement becomes occupied.
- Occupied settlements lose population, morale, food, and security.
- Occupied settlements gain damage and damaged structure flags.
- Pillager-occupied settlements can spawn patrols.
- Occupation banners are placed near occupied settlements.

### Recruiting Villagers

- Shift-right-click an adult villager to recruit it.
- Recruits are renamed with a `[Recruit]` prefix.
- Recruits persist across saves.
- Recruits can permanently die.
- Recruit deaths are tracked by the unit manager.

### Recruit Equipment

- Right-click your own recruit while holding an item to equip it.
- Right-click your own recruit with an empty hand to make it drop stored equipment.
- Shields equip to offhand.
- Other items equip to main hand.
- Equipped weapons override/default the recruit’s combat role.
- Enchanted weapons are preserved and used in combat.
- Weapon durability is consumed through normal item damage behavior.

### Recruit Combat

- Recruited villagers gain combat AI.
- Recruits target nearby hostile monsters.
- Recruits move into melee range and attack with their equipped weapon.
- Weapon enchantments can modify damage and apply post-hit effects.
- Recruits with shields attempt to block when threatened.

### Squads

- Squads are created from nearby recruited villagers.
- A squad has one leader and multiple members.
- Members follow leader-based formation offsets.
- Supported commands: follow, hold, patrol, defend, attack, assault, retreat.
- Supported formations: line, column, defensive ring.

### Config

- `regionShift`
  - Territory region size as a power of two in chunks. Default: `2`, meaning 4x4 chunks.

- `captureStep`
  - Capture/control progress changed per conflict tick. Default: `250`.

- `strategicTickSeconds`
  - How often pillagers evaluate border pressure. Default: `120`.

- `conflictTickSeconds`
  - How often active conflicts resolve a battle tick. Default: `10`.

- `squadSpawnRadius`
  - Player distance for nearby physical battles. Default: `128`.

- `settlementClaimRadius`
  - How many region steps a settlement claims outward. Default: `2`.

- `maxPhysicalSquadSize`
  - Maximum nearby pillager reinforcements for physical battles. Default: `6`.

- `squadTickInterval`
  - Server ticks between squad movement updates. Default: `5`.
