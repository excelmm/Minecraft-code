# Minecraft-code

## Start game
- Tick 0: 
  - team add mazeA
- Tick 1: 
  - team add mazeB
- Tick 2:
  - execute positioned ~-6 ~-12 ~-11 as @a[dx=17,dy=8,dz=22,limit=2] run team join mazeA @s
- Tick 3:
  - execute positioned ~-6 ~-12 ~-11 as @a[dx=17,dy=8,dz=22, team=!mazeA] run team join mazeB @s
- Tick 4:
  - gamemode spectator @r[limit=1,team=mazeA] 
  - gamemode spectator @r[limit=1,team=mazeB] 
- Tick 5:
  - title @a[gamemode=spectator] title {"text":"Help your friends!", "italic":true,"color":"gold"}
  - title @a[gamemode=spectator] title {"text":"Finish the maze!", "italic":true,"color":"gold"}
Tick 7:
  - scoreboard players set mazeDone mazeDone 0
  - scoreboard players set @a mazeDone 0
  - execute as @a at @s run spawnpoint @s ~ ~ ~
  - clone ~-10 ~-16 ~-6 ~5 ~-16 ~-6 ~-10 ~-12 ~-6 
  - setblock ~-50 ~-13 ~115 minecraft:netherrack
Tick 8:
  - execute positioned ~-6 ~-12 ~-11 run tp @a[team=teamB] ~-5 ~ ~18 (tp to mazes)
  - execute positioned ~-6 ~-12 ~-11 run tp @a[team=teamA] ~-5 ~ ~   (tp to mazes)
  - setblock ~-40 ~-11 ~-5 air (lever)
  - setblock ~-86 ~-12 ~-1 air (boss room entrance mechanism)
  - setblock ~-86 ~-12 ~-1 minecraft:redstone_block (boss room entrance mechanism)
  
  
## Escape Room entry
- Repeat - execute if score mazeDone mazeDone matches 5 run setblock ~ ~3 ~ minecraft:lever[facing=east]
  - Chain conditional - scoreboard players set mazeDone mazeDone 0

## Fireplace
- For the matches (to put in chest): give @p minecraft:flint_and_steel{display:{Name:'{"text":"Match","color":"gold","bold":true}'}}
- Repeat - execute positioned ~-2 ~4 ~1 if entity @e[nbt={Item:{id:"minecraft:ice"}},distance=..2] run kill @e[nbt={Item:{id:"minecraft:ice"}}]
  - Chain conditional - execute positioned ~-2 ~3 ~3 run summon minecraft:item ~ ~ ~ {Item:{id:"minecraft:fishing_rod",Count:5,tag:{Enchantments:[{id:lure,lvl:3}]}}}
  
- Repeat - execute as @p[distance=..4,scores={mazeDone=0}] if entity @s run scoreboard players add @s mazeDone 1
  - Chain conditional - scoreboard players add mazeDone mazeDone 1
  
## Chest at the end of parkour
- Fill with:
- give @p ice{display:{Name:'{"text":"Fuel","color":"gray","bold":true,"italic":true}'}}
- give @p diamond{display:{Name:'{"text":"Sacrificial token","color":"gold","bold":true,"italic":true}',Lore:['{"text":"Keep this for the boss fight!"}']}} 26 

## Gear equipper before boss fight



## Make armor stands invulnerable
- data merge entity @e[type=minecraft:armor_stand,limit=1,sort=nearest] {Invulnerable:1b,DisabledSlots:2096896}

## Make item frames invulnerable
- data merge entity @e[type=minecraft:item_frame,limit=1,sort=nearest] {Invulnerable:1b}
