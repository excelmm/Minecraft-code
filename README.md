# Minecraft-code

## Start game
- Tick 0: 
  - team add mazeA
- Tick 1: 
  - team add mazeB
- Tick 2:
  - execute positioned ~-6 ~-12 ~-11 as @a[dx=17,dy=8,dz=22,limit=2] run team join mazeA1 @s **Game dependent**
- Tick 3:
  - execute positioned ~-6 ~-12 ~-11 as @a[dx=17,dy=8,dz=22, team=!mazeA] run team join mazeB1 @s **Game dependent**
- Tick 4:
  - gamemode spectator @r[limit=1,team=mazeA1] **Game dependent**
  - gamemode spectator @r[limit=1,team=mazeB1] **Game dependent**
- Tick 5:
  - title @a[tag=game1,gamemode=spectator] title {"text":"Help your friends!", "italic":true,"color":"gold"} **Game dependent**
  - title @a[tag=game1,gamemode=!spectator] title {"text":"Finish the maze!", "italic":true,"color":"gold"} **Game dependent**
- Tick 7:
  - scoreboard players set mazeDone1 mazeDone 0 **Game dependent**
  - scoreboard players set @a[tag=game1] mazeDone 0 **Game dependent**
  - execute as @a[tag=game1] at @s run spawnpoint @s ~ ~ ~ **Game dependent**
  - clone ~-10 ~-16 ~-6 ~5 ~-16 ~-6 ~-10 ~-12 ~-6 
  - setblock ~-50 ~-13 ~115 minecraft:netherrack
- Tick 8:
  - execute positioned ~-6 ~-12 ~-11 run tp @a[team=teamB1] ~-5 ~ ~18 (tp to mazes) **Game dependent**
  - execute positioned ~-6 ~-12 ~-11 run tp @a[team=teamA1] ~-5 ~ ~   (tp to mazes) **Game dependent**
  - setblock ~-40 ~-11 ~-5 air (lever)
  - setblock ~-86 ~-12 ~-1 air (boss room entrance mechanism)
  - setblock ~-86 ~-12 ~-1 minecraft:redstone_block (boss room entrance mechanism)
  
## Entrance to puzzle room
- Repeat - execute if score mazeDone1 mazeDone matches 5 run setblock ~ ~3 ~ minecraft:lever[facing=east] **Game dependent**
  - Chain conditional - scoreboard players set mazeDone1 mazeDone 0 **Game dependent**
  - Chain conditional - /spawnpoint @a[tag=game1] ~-5 ~1 ~3 **Game dependent**
  - Chain conditional - title @a[tag=game1] title {"text":"GO GO GO!!!","color":"gold","italic":true} **Game dependent**

- Repeat - execute as @p[distance=..4,scores={mazeDone=0}] if entity @s run scoreboard players add @s mazeDone 1
  - Chain conditional - scoreboard players add mazeDone1 mazeDone 1 **Game dependent**
  
  
## Escape Room entry
- Repeat - execute if score mazeDone1 mazeDone matches 5 run setblock ~ ~3 ~ minecraft:lever[facing=east] **Game dependent**
  - Chain conditional - scoreboard players set mazeDone1 mazeDone 0   **Game dependent**
- Repeat - execute as @p[distance=..4,scores={mazeDone=0}] if entity @s run scoreboard players add @s mazeDone 1
  - Chain conditional - scoreboard players add mazeDone1 mazeDone 1 **Game dependent**

## Puzzle 1 - Chest at the end of parkour
- Fill with:
- give @p ice{display:{Name:'{"text":"Fuel","color":"gray","bold":true,"italic":true}'}}
- give @p diamond{display:{Name:'{"text":"Sacrificial token","color":"gold","bold":true,"italic":true}',Lore:['{"text":"Keep this for the boss fight!"}']}} 26 
- Repeat - execute if block ~ ~-6 ~ minecraft:chest{Items:[]} run setblock ~ ~-6 ~ air
  - Chain conditional - title @a subtitle {"text":"Keep going!"}
  - Chain conditional - title @a title {"text":"Puzzle 1 complete!", "color":"green", "bold":true,"italic":true}

## Puzzle 2 - Fireplace
- For the matches (to put in chest): give @p minecraft:flint_and_steel{display:{Name:'{"text":"Match","color":"gold","bold":true}'}}
- Repeat - execute positioned ~-2 ~4 ~1 if entity @e[nbt={Item:{id:"minecraft:ice"}},distance=..2] run kill @e[nbt={Item:{id:"minecraft:ice"}}]
  - Chain conditional - execute positioned ~-2 ~3 ~3 run summon minecraft:item ~ ~ ~ {Item:{id:"minecraft:fishing_rod",Count:5,tag:{display:{Lore:['{"text":"Share with your friends!"}']},Enchantments:[{id:lure,lvl:3}]}}}
  - title @a[tag=game1] subtitle {"text":"Good job!"} **Game dependent**
  - title @a[tag=game1] title {"text":"Puzzle 2 complete!", "color":"blue","bold":true,"italic":true} **Game dependent**
  
## Puzzle 3 - Tom Holland
- Repeat - execute if entity @e[type=cat, distance=..20, tag=!adult] run say hi
  - Chain conditional - tag @e[type=cat, tag=!adult,distance=..20] add adult
  - Chain conditional - clone ~-3 ~ ~ ~-3 ~ ~ ~-3 ~2 ~
  - title @a[tag=game subtitle {"text":"Jiayoussss"} **Game dependent**
  - title @a title {"text":"Puzzle 3 complete!", "color":"red","bold":true,"italic":true} **Game dependent**
  
## Puzzle 4 - Target Practice
- title @a[tag=game1] subtitle {"text":"One half of the door has opened!"} **Game dependent**
- title @a[tag=game1] title {"text":"Puzzle 4 complete!","color":"gold","italic":true,"bold":true} **Game dependent**

## Puzzle 5 - Sword combinations
- title @a[tag=game1] subtitle {"text":"One half of the door has opened!"} **Game dependent**
- title @a[tag=game1] title {"text":"Puzzle 5 complet!","color":"lime","bold":true,"italic":true} **Game dependent**

## Gear equipper before boss fight
- gamerule mobGriefing false
- difficulty normal
- execute positioned ~-18 ~18 ~-1 run summon wither ~ ~ ~
  - Chain tag @e[distance=..100,type=wither] add monster
- give @a[tag=!admin,distance=..6] bow{Enchantments:[{id:power,lvl:4}]}
  - Chain give @a[tag=!admin,distance=..6] arrow 128
  - Chain spawnpoint @a[tag=game1] ~7 ~5 ~-1 **Game dependent**
- give @a[tag=!admin,distance=..6] minecraft:netherite_sword
  - Chain replaceitem entity @a[tag=!admin,distance=..6] armor.head minecraft:iron_helmet
  - Chain replaceitem entity @a[tag=!admin,distance=..7] armor.feet minecraft:iron_boots
- give replaceitem entity @a[tag=!admin,distance=..6] armor.chest minecraft:iron_chestplate
  - Chain replaceitem entity @a[tag=!admin,distance=..6] armor.legs minecraft:iron_leggings
  - Chain effect give @a[tag=!admin,distance=..7] minecraft:regeneration 10000 5
  
## Final room
- Player detection: execute if entity @a[distance=..5,tag=!admin] run title @a[tag=game1] title {"text":"Lights please!","color":"gold","bold":true,"italic":true} **Game dependent**

## Make armor stands invulnerable
- data merge entity @e[type=minecraft:armor_stand,limit=1,sort=nearest] {Invulnerable:1b,DisabledSlots:2096896}

## Make item frames invulnerable
- data merge entity @e[type=minecraft:item_frame,limit=1,sort=nearest] {Invulnerable:1b}

## Give placable end rods
- give @p end_rod{CanPlaceOn:["stone"],display:{Name:'{"text":"Light Stick","color":"gold","bold":true,"italic":true}', Lore:['{"text":"Hmmmmm where shall I place these?"}']}}
