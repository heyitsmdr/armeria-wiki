---
title: Cartography
description: 
published: true
date: 2021-02-13T18:00:46.539Z
tags: 
editor: markdown
dateCreated: 2020-11-20T16:47:11.761Z
---

# Overview
Job description.
# Perks
| Level | Description |
|:-:|:-|
|1| A cool perk description here. |
|3| Another awesome perk description right here. |

# Old Document Dump
Using this skill, a character can create maps of an area, which can be shared (sold or given) to other characters. The player can initiate the creation of a map by having the required materials in their inventory, and executing the /map create material command, where the player can specify which paper type to use for the map.

Once the map is created, it is placed in the character’s inventory, named Incomplete Map (#), where the number is how many more grid spaces the map can hold. This number is to be updated after each new tile is added to the map.

Adding a tile to the map is done automatically upon the character’s movement, and a message is displayed the character, letting them know the tile has been added, like this:

PC has added a new tile [Test Area,1,0,0] to the map. The map can hold # more rooms.

Maps are limited to the area they are originally created in. If the character moves to a different area during the mapping process, they will be notified, and the map creation will be paused temporarily. To pause or resume map creation manually, the player can execute the commands:

/map pause
/map resume

	A room that has been recorded on the map can be given extra details, but it is not required. Those details include:
Room Name
Room Keywords
Those attributes for the given room within the map can then be used by the owner of the map when searching the map. (See System - Exploration - Maps)

Once finished, the player can stop creating the map by executing the /map finish Name command. The name provided in this command sets the item name within their inventory.

Only one (1) Incomplete Map can be in a character’s inventory at one time. If the player tries to create an additional map, or they attempt to withdraw another one from storage, they will receive an error letting them know:

You cannot have multiple Incomplete Maps in your inventory at one time. If you would like to create or modify a different map, you will need to either finish the one you have now, or deposit it somewhere.

The maximum size of a map is governed by the character’s Cartography level, as well as the materials used when initially creating the Incomplete Map.