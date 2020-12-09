---
title: Mobs
description: 
published: true
date: 2020-12-09T20:47:11.866Z
tags: 
editor: markdown
dateCreated: 2020-12-01T20:36:49.400Z
---

# Mobs

**Mobs** (short for "Mobiles") are the non-player characters (NPCs) and creatures of the game world. They are spawnable, scriptable entities that exist in rooms. They can be fought, killed, interacted with, given items, and much more. Mobs are what brings the game world alive.

## Creating Mobs

When developing areas for Armeria, you will likely be creating quite a few Mobs. However, you should do your due-diligence and look through the existing mobs to see if one exists that suites your needs. You can do so by taking a look at:

```
/mob list
```

### Scripts

Mobs support scripting via the [Lua](https://www.lua.org/) scripting language. Just about every mob will have a script of some sort as these are what make mobs "come alive".

To open the script editor, first open the object editor for the mob:

```
/mob edit <name>
```

Next, click on `[Edit Script]` next to the `script` property and this will open the script editor in a pop-up window. If you don't see anything, ensure your browser is not blocking popups from Armeria.

### Movement

Mobs have the ability to move around the game world. To set up mob movement, create an item of type **mob-breadcrumb**. Spawn several instances of the breadcrumb and drop them in each room that you'd like the mob to walk between. These breadcrumbs should have `visible: false` set so that players cannot see them.

Next, you'll need to instruct the mob to follow that particular breadcrumb. You can do this by setting the `followCrumb: <crumb name>` property on the mob. By default, the mob will randomly follow the crumbs as long as there's always an adjacent room with a crumb to follow.

As for speed, you can use the `followSpeed` property on the mob. This setting relates to how many "mob movement ticks" you want the mob to wait for before making its next move. Mob movement ticks occur every 5 seconds. As an example, setting `followSpeed: 1` will cause the mob to move every 5 seconds. Furthermore, setting `followSpeed: 12` will cause the mob to make a move once a minute. You can use values between **1 - 60**.

**Mob stuck?** If a mob is set to follow a breadcrumb and there are no valid breadcrumbs for it to follow, an automated message will be sent to the **Builders** channel.