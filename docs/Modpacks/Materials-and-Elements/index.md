---
title: "Materials & Elements"
---


# Materials & Elements

GregTech has its own material system based on chemical elements.

Materials are composed of chemical elements and/or other materials.  
Each material can have different items (and blocks), such as ingots, dusts, plates, wires, ores, etc.

## A note about registration
Order matters when you are registring a new material. If you reference a material by `.components()`, you must either make sure the material is either created before or when on another file loaded first.
