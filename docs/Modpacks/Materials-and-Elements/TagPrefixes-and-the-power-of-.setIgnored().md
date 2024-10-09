---
title: TagPrefixes and the power of .setIgnored()
---
## What is a TagPrefix?
TagPrefixes are GTCEu Modern's way of streamlining applying item and block tags to Materials, along with some other functions. The `TagPrefix` class, 
available for use in startup and server scripts, contains a number of predefined TagPrefixes that 
associate potentially everything from drill heads to flawless gemstones with a material. A common and easy-to-understand example is `TagPrefix.ingot`, 
which associates with all Materials that have an IngotProperty and thus an associated ingot item, including custom ones defined via KubeJS. 
TagPrefixes provide localization, item and block tagging, and influence many crafting recipes, and are integral to the functioning of GTCEu's material definition system.

!!! tip "What TagPrefixes are there?"
    A list of all availabe TagPrefixes can be found in GTCEu Modern's GitHub or in the .JAR file, in the class `TagPrefix`.

## What is .setIgnored()?

While trawling thorugh GTCEu Modern's codebase, or simply by playing Minecraft, you may have noticed that GTCEu Modern treats some vanilla materials differently.
For example, iron ingots are a vanilla item, yet GTCEu Modern does not create a duplicate iron ingot, as its Material definition would suggest it were to do.
Instead, the GTCEu Modern Material entry for iron treats the vanilla iron ingots as the material's ingot, and thus produces no duplicates.
This functionality is governed by TagPrefixes, and can also be harnessed by packmakers for their own custom items, or when writing compatibility between GTCEu Modern and another mod.

## Okay, but how do I use this?

This functionality can be leveraged in the material modification event, which is a startup event.
The material modification event occurs in Minecraft's boot sequence after Material registration is finalized, but before the Material registry is closed; you won't be able to define any new Materials using it.
The following calls are available for each TagPrefix:
  - `.setIgnored()` with one input parameter: Takes a `Material` as input and prevents GTCEu from associating that specific TagPrefix with that Material.
  - `.setIgnored()` with two input parameters: Takes a `Material` and an `Item` or `ItemStack` as input; causes GTCEu to treat the passed ItemStack as what the TagPrefix would have originally generated for the Material.
  - `.removeIgnored()`: takes a `Material` as input and re-enables generation of the item associated with the TagPrefix for that material.

A more illustrative example, using some Applied Energistics 2 items:

  ```js title="setignored_usage_example.js"
  GTCEuStartupEvents.materialModification(event => { // (1)
      TagPrefix.gemChipped.setIgnored(GTMaterialRegistry.getMaterial("fluix_crystal")) // (2)
      TagPrefix.rock.setIgnored(GTMaterialRegistry.getMaterial("sky_stone"), Item.of("ae2:sky_stone").getItem()) // (3)
      TagPrefix.ingot.removeIgnored(GTMaterials.Iron) // (4)
  })
  ```
  1. This event has no methods such as `event.create()`, as it is not intended to be used to create anything, only modify pre-existing Material entries.
  2. This call prevents GTCEu Modern from creating a chipped gem variant of the custom 'fluix_crystal' Material.
  3. This call makes GTCEu Modern treat AE2's Sky Stone block as a rock type that is associated with the custom 'sky_stone' Material.
  4. This call makes GTCEu Modern stop considering vanilla iron ingots as the ingots for GTCEu Modern's iron Material, allowing it to generate a duplicate iron ingot.

The `Material` for which you are adjusting the TagPrefix must be registered in GTCEu Modern's material registry; if this material is custom, this is done using `GTCEuStartupEvents.rgistry()`, as depicted in these docs.
