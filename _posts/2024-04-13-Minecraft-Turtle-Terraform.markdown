---
title: "Minecraft Turtle Terraform"
date: 2024-04-13
tags: [Lua, Automation, Minecraft, ComputerCraft, Turtles]
---

### Problem
I need a nice flat area to build on, but digging and terraforming takes forever and is boring

### Solution
This script causes a Turtle to navigate a square area defined by the user, it flattens the area as much as possible and places a block down when possible to also fill holes.

### Impact
useful for creating large flat spaces, multiple can be run over small areas to quickly create large building areas.

## Key Functions

### smartRefuel()
a useful part of any turtle operation loop, this causes the turtle to stop and check it's fuel levels to ensure they remain above a configurable threshold, it will search it's inventory for anything it considers fuel, and top up with that item.

### gu() gd() gf()
these are strong movement functions which add to the turtle default movement.  each one adds a loop which causes the turtle to dig whenever the movementn fails, this ensures that environmental changes do not prevent the turtle from moving.  gu() and gd() add local y tracking so the turtle can keep track of the level plane it's creating.  gf() creates the pattern which allows it to cut down trees or hills, it attempts to move forward and if there is an obstacle it moves up, this repeats until it can successfully move forward, once it does it digs down back to y level 0

## Design and limitations
one notable limitation to this design is that the turtle cannot detect a cave that is 2 or more blocks higher than it's y level.  The trade of here is speed.  such caves in typical use cases are quite rare, and because turtles can't "see" the alternative would be a lot of wasted upward movement.  currently it uses dirt or cobblestone, but this could be expanded to use a list of blocks.  finally, smartrefuel() only runs at the beginning of the operation, so a very large dig could cause the Turtle to inadvertantly run out of fuel.

## Challenges
getting the strong movement functions and the sweeping motion to work together seemlessly was a challenge.  Turtle movement is not the most human intuitive thing and so there was a lot of trial and error involved to get that just right.