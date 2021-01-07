# Minecraft-code

## Clear all tags (entrance to lobby room)
- execute positioned ~ ~2 ~ as @p[tag=!admin,distance=..1] run tag @s add removeTag **Game dependent**

## Lobby locker
- execute if entity @e[distance=..2, tag=!admin] run setblock ~ ~2 ~2 minecraft:red_nether_brick_wall
- execute positioned ~ ~ ~1 run fill ~2 ~2 ~2 ~-2 ~2 ~-2 minecraft:prismarine_wall replace minecraft:red_nether_brick_wall
- execute positioned ~ ~ ~2 as @e[distance=..2, tag=!admin] run tag @s add game1 **Game dependent**

## Start game
- Tick 0: 
  - team add mazeA1 **Game dependent**
- Tick 1: 
  - team add mazeB1 **Game dependent**
  - team leave @a[tag=game1] **Game dependent**
  - clear @a[tag=game1] **Game dependent**
  - scoreboard objectives add players dummy
  - team empty mazeA1 **Game dependent**
  - team empty mazeB1 **Game dependent**
- Tick 2:
  - execute as @a[tag=game1,limit=3] run team join mazeA1 @s **Game dependent**
- Tick 3:
  - execute as @a[tag=game1,team=!mazeA1] run team join mazeB1 @s **Game dependent**
  - scoreboard objectives add mazeDone dummy
  - scoreboard objectives add finished dummy
  - scoreboard players set players1 players 0 **Game dependent**
- Tick 4:
  - scoreboard players set mazeDone1 mazeDone 0 **Game dependent**
  - scoreboard players set @a[tag=game1] mazeDone 0 **Game dependent**
  - gamemode spectator @r[team=mazeA1] **Game dependent**
  - gamemode spectator @r[team=mazeB1] **Game dependent**
- Tick 5:
  - title @a[tag=game1,gamemode=spectator] title {"text":"Help your friends!", "italic":true,"color":"gold"} **Game dependent**
  - title @a[tag=game1,gamemode=!spectator] title {"text":"Finish the maze!", "italic":true,"color":"gold"} **Game dependent**
- Tick 7:
  - execute as @a[tag=game1] at @s run spawnpoint @s ~ ~ ~ **Game dependent**
  - clone ~-10 ~-16 ~-6 ~5 ~-16 ~-6 ~-10 ~-12 ~-6 
  - setblock ~-50 ~-13 ~115 minecraft:netherrack
  - execute as @a[tag=game1] run scoreboard players add players1 players 1 **Game dependent**
  - scoreboard players set finished1 finished 0 **Game dependent**
  - scoreboard players set @a[tag=game1] finished 0 **Game dependent**
- Tick 8:
  - tp @a[team=mazeA1] ~-15 ~-12 ~5 (tp to mazes) **Game dependent**
  - tp @a[team=mazeB1] ~-14 ~-12 ~-13 (tp to mazes) **Game dependent**
  - setblock ~-40 ~-11 ~-5 air (lever)
  - setblock ~-86 ~-12 ~-1 air (boss room entrance mechanism)
  - setblock ~-86 ~-12 ~-1 minecraft:redstone_block (boss room entrance mechanism)
  - summon cat ~-80 ~-12 ~-20 {CustomName:'{"text":"Tom"}',Invulnerable:1b,Tags:["adult"]}
  - summon cat ~-81 ~-12 ~-20 {CustomName:'{"text":"Holland"}',Invulnerable:1b,Tags:["adult"]}
  
## Exit maze
- execute as @p at @s run tp @a[team=mazeA1] @s **Game dependent**
- gamemode adventure @a[team=mazeA1] **Game dependent**
- execute as @p at @s run tp @a[team=mazeB1] @s **Game dependent**
- gamemode adventure @a[team=mazeB1] **Game dependent**
  
## Entrance to puzzle room
- Repeat - execute if score mazeDone1 mazeDone = players1 players run setblock ~ ~3 ~ minecraft:lever[facing=east] **Game dependent**
  - Chain conditional - scoreboard players set mazeDone1 mazeDone 0 **Game dependent**
  - Chain conditional - /spawnpoint @a[tag=game1] ~-5 ~1 ~3 **Game dependent**
  - Chain conditional - title @a[tag=game1] title {"text":"GO GO GO!!!","color":"gold","italic":true} **Game dependent**

- Repeat - execute as @p[distance=..4,scores={mazeDone=0}] if entity @s run scoreboard players add @s mazeDone 1
  - Chain conditional - scoreboard players add mazeDone1 mazeDone 1 **Game dependent**
  
## Floating text
- /summon armor_stand ~ ~2 ~ {Invisible:1b,Invulnerable:1b,NoGravity:1b,Marker:1b,CustomName:"{\"text\":\"Whereever I face, my sword shall point.\",\"color\":\"gold\",\"bold\":\"true\",\"italic\":true}",CustomNameVisible:1b}

## Puzzle 1 - Chest at the end of parkour
- Fill with:
- give @p ice{display:{Name:'{"text":"Fuel","color":"gray","bold":true,"italic":true}'}}
- give @p diamond{display:{Name:'{"text":"Sacrificial token","color":"gold","bold":true,"italic":true}',Lore:['{"text":"Keep this for the boss fight!"}']}} 26 
- Repeat - execute if block ~ ~-6 ~ minecraft:chest{Items:[]} run setblock ~ ~-6 ~ air
  - Chain conditional - title @a[tag=game1] subtitle {"text":"Keep going!"} **Game dependent**
  - Chain conditional - title @a[tag=game1] title {"text":"Puzzle 1 complete!", "color":"green", "bold":true,"italic":true} **Game dependent**

## Puzzle 2 - Fireplace
- For the matches (to put in chest): give @p minecraft:flint_and_steel{display:{Name:'{"text":"Match","color":"gold","bold":true}'},CanPlaceOn:["netherrack"]}
- Repeat - execute positioned ~-2 ~4 ~1 if entity @e[nbt={Item:{id:"minecraft:ice"}},distance=..2] run kill @e[nbt={Item:{id:"minecraft:ice"}}]
  - Chain conditional - give @a[tag=game1] minecraft:fishing_rod{display:{Lore:['{"text":"Share with your friends!"}']},Enchantments:[{id:lure,lvl:3}]} 1 **Game dependent**
  - title @a[tag=game1] subtitle {"text":"Good job! You all have fishing rods now :)"} **Game dependent**
  - title @a[tag=game1] title {"text":"Puzzle 2 complete!", "color":"blue","bold":true,"italic":true} **Game dependent**
  
## Puzzle 3 - Tom Holland
- Repeat - execute if entity @e[type=cat, distance=..20, tag=!adult] run say hi
  - Chain conditional - tag @e[type=cat, tag=!adult,distance=..20] add adult
  - Chain conditional - clone ~-3 ~ ~ ~-3 ~ ~ ~-3 ~2 ~
  - title @a[tag=game1] subtitle {"text":"Jiayoussss! Open the chest for bows and arrows!"} **Game dependent**
  - title @a[tag=game1] title {"text":"Puzzle 3 complete!", "color":"red","bold":true,"italic":true} **Game dependent**
  
## Puzzle 4 - Target Practice
- title @a[tag=game1] subtitle {"text":"One half of the door has opened!"} **Game dependent**
- title @a[tag=game1] title {"text":"Puzzle 4 complete!","color":"gold","italic":true,"bold":true} **Game dependent**

## Puzzle 5 - Sword combinations
- title @a[tag=game1] subtitle {"text":"One half of the door has opened!"} **Game dependent**
- title @a[tag=game1] title {"text":"Puzzle 5 complet!","color":"lime","bold":true,"italic":true} **Game dependent**

## Gear equipper before boss fight
- gamerule mobGriefing false
- difficulty normal
- execute unless entity @e[tag=monster,distance=..50] positioned ~-18 ~18 ~-1 run summon minecraft:zombified_piglin ~ ~1 ~ {HandItems:[{Count:1,id:netherite_sword},{}],ArmorItems:[{Count:1,id:diamond_boots,tag:{Enchantments:[{id:protection,lvl:4}]}},{Count:1,id:diamond_leggings,tag:{Enchantments:[{id:protection,lvl:4}]}},{Count:1,id:diamond_chestplate,tag:{Enchantments:[{id:protection,lvl:4}]}},{Count:1,id:diamond_helmet,tag:{Enchantments:[{id:protection,lvl:4}]}}],CustomName:"\"Covid-19\"",Tags:["game1","monster"],Attributes:[{Name:"generic.maxHealth",Base:100}],Health:100}
- give @a[tag=!admin,distance=..6] bow{Enchantments:[{id:power,lvl:4}]}
  - Chain give @a[tag=!admin,distance=..6] arrow 128
  - Chain spawnpoint @a[tag=game1] ~7 ~5 ~-1 **Game dependent**
- give @a[tag=!admin,distance=..6] minecraft:netherite_sword
  - Chain replaceitem entity @a[tag=!admin,distance=..6] armor.head minecraft:iron_helmet
  - Chain replaceitem entity @a[tag=!admin,distance=..7] armor.feet minecraft:iron_boots
- give replaceitem entity @a[tag=!admin,distance=..6] armor.chest minecraft:iron_chestplate
  - Chain replaceitem entity @a[tag=!admin,distance=..6] armor.legs minecraft:iron_leggings
  - Chain effect give @a[tag=!admin,distance=..7] minecraft:regeneration 10000 5
  
## COVID-19 Slain
- Repeat - execute if entity @e[distance=..50,tag=monster] run setblock ~ ~-1 ~ redstone_block
  - Repeat - bossbar set minecraft:bossbar1 visible false **Game dependent**
  - Chain conditional - bossbar set minecraft:bossbar1 players @a[tag=game1] **Game dependent**
- Repeat - execute unless entity @e[distance=..50,tag=monster] run setblock ~ ~1 ~ air
  - Chain conditional - title @a[tag=game1] subtitle "Congratulations! You're almost done" **Game dependent**
  - Chain conditional - title @a[tag=game1] title {"text":"COVID-19 is dead!!","color":"dark_red","bold":true,"italic":true} **Game dependent**
  - Repeat - bossbar set minecraft:bossbar1 visible true **Game dependent**
  
## After COVID-19 slain
- clear @a[tag=game1] **Game dependent**
  
## Final room
- Player detection: Repeat - execute as @a[tag=game1,tag=!admin,distance=..7,scores={finished=0}] run scoreboard players set @s finished 1
  - Chain conditional - scoreboard players add finished1 finished 1 **Game dependent**
- Repeat - execute unless score finished1 finished matches 0 if score finished1 finished = players1 players run fill ~-2 ~-7 ~-2 ~2 ~-7 ~4 air **Game dependent**
  - Chain conditional - title @a[tag=game1] title {"text":"WATCH OUT!!!","color":"dark_red"} **Game dependent**
  - Chain conditional - give @a[tag=game1] torch{CanPlaceOn:["dirt"]} 128 **Game dependent**

## Maze TPs
- tp @p ~-20 ~1 ~1
- tp @p ~-29 ~1 ~11
- title @p subtitle {"text":"You have escaped!!!","bold":true}
  - Chain execute positioned ~-1 ~ ~ run title @p title {"text":"Congratulations!","color":"gold","bold":true,"italic":true}
  - execute positioned ~-2 ~ ~ run tp @p ~119 ~22 ~44

## Make armor stands invulnerable
- data merge entity @e[type=minecraft:armor_stand,limit=1,sort=nearest] {Invulnerable:1b,DisabledSlots:2096896}

## Make item frames invulnerable
- data merge entity @e[type=minecraft:item_frame,limit=1,sort=nearest] {Invulnerable:1b}

## Give placable end rods
- give @p end_rod{CanPlaceOn:["stone"],display:{Name:'{"text":"Light Stick","color":"gold","bold":true,"italic":true}', Lore:['{"text":"Hmmmmm where shall I place these?"}']}}
