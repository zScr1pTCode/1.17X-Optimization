# 1.17X-Optimization
Optimization | PaperMC

## Intro | 1.17X

**Spigot** and **Paper** offer settings that greatly **improve performance.** This guide breaks down suggested values that get the most out of your server without compromising gameplay.

### __Mᴀᴘ Pʀᴇ-Gᴇɴ__
> Map pre-generation is critical to lag removal. Do not use ClearLag, that plugin does not fix lag..

Plugin: **Chunky**

- Download [Here](https://www.spigotmc.org/resources/chunky.81534/)

- Guide? [Wiki](https://github.com/pop4959/Chunky/wiki)




### __Bukkit.yml__

```
Spawn-limits:
 monsters: 38
 animals: 12
 water-animals: 7
 ambient: 1
```
```
chunk.gc:
 period-in-ticks: 400
```
> ➫ This unloads vacant chunks faster. Ticking fewer chunks means less TPS consumption.

```
ticks-per:
 animal-spawns: 350
 monster-spawns: 5
 water-spawns: 14
 water-ambient-spawns: 21
 ambient-spawns: 28
 autosave: 6000
 ```
> ➫ This enables Bukkit's world saving and how often it runs (in ticks). It should be 6000 by default, just double check it is not 0 (disabled).

**Note:** If you use your server or a plugin to run saves, **STOP!** They just run the very obsolete `/save-all` command.

**Worldsave Lag:** Lag spikes from Worldsave? You might consider Paper's lag-free saving.


### __Spigot.yml__

```
settings:
  save-user-cache-on-stop-only: true
  log-villager-deaths: false
```
> ➫ Should the server constantly save user data (false) or delay that task until a stop/restart (true)? This is nice TPS savings on Spigot (less on Paper since it's more efficient).

**Note:** Take regular backups to avoid data loss in the rare event of a fatal crash.

```
max-tick-time:
  tile: 1000
  entity: 1000
```
> ➫ 1000 disables this feature. The small TPS savings is not worth the potential damage.

```
mob-spawn-range: 6
```
> ➫ This sets the max mob spawning distance (in chunks) from players. After limiting spawns in Bukkit, this will condense mobs to mimic the appearance of normal rates.

```
entity-activation-range:
  animals: 16
  monsters: 24
  raiders: 32
  misc: 8
  water: 4
  villagers: 19
  flying-monsters 9
  tick-inactive-villagers: false
```
> ➫ Entities past this range will be ticked less often. Avoid setting this too low or you might break mob behavior (mob aggro, raids, etc).

**Note:** Villagers should be left alone (*if possible*) to protect mechanics.

> ➫ Enabling "`tick-inactive-villagers: false`" this prevents the server from ticking villagers outside the activation range.

**Note:** Vanilla behavior ticks all villagers in loaded chunks. Enable villagers-active-for-panic to save some iron farms from breaking.

```
merge-radius:
  item: 4.0
  exp: 6.0
```
> ➫ Merging items means less ground item ticking. Higher values allow more items to be swept into piles.

**Note:** Merging will lead to the illusion of items disappearing as they merge together. A minor annoyance.

```
nerf-spawner-mobs: true
```
> ➫ When enabled, mobs from spawners will not have AI (will not swim/attack/move). This is big TPS savings for massive mob farms, but also messes with behavior. A farm limiter plugin might be a better solution.

**Note:** Paper has an option to force nerfed mobs to jump/swim. This fixes water push farms.

```
item-despawn-rate: 6000
```

> ➫ Similar to item-despawn-rate, but for arrows. Some servers may want to keep arrows on the ground longer, but most will have no complaints if removed faster.

**Note:** Paper has settings to reduce the gameplay impact of arrow removal. Leave this near default if you use Paper's arrow options.

```
arrow-despawn-rate: 300
```
> ➫ Similar to item-despawn-rate, but for arrows. Some servers may want to keep arrows on the ground longer, but most will have no complaints if removed faster.

**Note:** Paper has settings to reduce the gameplay impact of arrow removal. Leave this near default if you use Paper's arrow options.



## __Paper.yml__
```
max-auto-save-chunks-per-tick: 6
```

```
optimize-explosions: true
```
> Paper has a very efficient algorithm for explosions with no impact to gameplay.

```
mob-spawner-tick-rate: 2
```

```
disable-chest-cat-detection: true
```

```
container-update-tick-rate: 3
```

```
grass-spread-tick-rate: 4
```

```
despawn-ranges:
  soft: 28
  hard: 96
```

`Soft` = The distance (in blocks) from a player where mobs will be periodically removed.

`Hard` = Distance where mobs are removed instantly.

> ➫ Lower ranges clear background mobs and allow more to be spawned in areas with player traffic. This further reduces the gameplay impact of reduced spawning (***bukkit.yml***).

```
hopper:
  disable-move-event: true
```
- **Warning:** Plugins that listen for InventoryMoveItemEvent will break.

```
non-player-arrow-despawn-rate: 120
creative-arrow-despawn-rate: 120
```

```
prevent-moving-into-unloaded-chunks: true
```

> ➫ Prevents players from entering an unloaded chunk (due to lag), which causes more lag. The true setting will set them back to a safe location instead.

**Note:** If you did not pre-generate your world (*what's wrong with you?!*) this setting is critical.

```
use-faster-eigencraft-redstone: true
```

```
armor-stands-tick: true
```

```
per-player-mob-spawns: true
```
> ➫ This implements singleplayer spawning behavior instead of Bukkit's random algorithms. This prevents the actions of others (**i.e. Massive farms**) from impacting the server's spawn rates.

**Note:** If you lowered `spawn-limits` in Bukkit and notice shortages of animals and monsters, consider bumping those back up until you find a happy place.

```
alt-item-despawn-rate: true
```
> ➫ Remove certain item drops faster (or slower) than the item-despawn-rate set in Spigot. This lets you avoid ticking massive piles of garbage.

- Example of despawning **cobblestone** and **netherrack** in **15** seconds:
```
enabled: true
items:
  COBBLESTONE: 300
  NETHERRACK: 300
```

```
no-tick-view-distance: 8
```

```
anti-xray:
  enabled: false
```
> It may cause TPS drops.


## __Server.Properties__
```
view-distance: 8
network-compression-threshold: 512
```
