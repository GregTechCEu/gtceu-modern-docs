---
title: "Adding Stone Types"
---


# Adding Stone Types for Ore Blocks

In a modpack, you may want to add your own stone types in order to integrate GT's ore generation with blocks from other mods.

To do so, you need to register a tag prefix for your ore, add a language key, as well as allowing your ores to actually generate.


## Files

For example purposes, this guide uses the block "Blockium" (ID: `my_mod:blockium`).  
Replace this with the block you want to add ores for.

```js title="startup_scripts/ore_types.js"
GTCEuStartupEvents.registry('gtceu:tag_prefix', e => {
    stoneTypes.forEach(type => {
        e.create('blockium', 'ore') // (1)
            .stateSupplier(() => Block.getBlock('my_mod:blockium').defaultBlockState()) // (2)
            .unificationEnabled(true)
            .materialIconType(GTMaterialIconType.ore)
            .generationCondition(ItemGenerationCondition.hasOreProperty)
    })
})
```

1. The first parameter for `create()` is the name that corresponds to your stone type. The second parameter is **always** `'ore'`!
2. For `Block.getBlock()` you must use the stone type's block ID as a parameter.


```json title="assets/gtceu/lang/en_us.json"
{
    "tagprefix.blockium": "Blockium %s Ore"
}
```


## Generating the Ores

To make your ores actually generate in the world, you have several options.
If you just want to stick to ore generation in the default dimensions, the easiest way to achieve this is adding your new ore base blocks to one of the following block tags:


- **Overworld:** `minecraft:stone_ore_replaceables` or `minecraft:deepslate_ore_replaceables`
- **Nether:** `minecraft:nether_carver_replaceables`
- **The End:** `forge:end_stone_ore_replaceables` on forge / `c:end_stone_ore_replaceables` on fabric

??? example "Adding blocks to a tag"
    ```js title="server_scripts/ore_type_tags.js"
    ServerEvents.tags('block', event => {
        event.add('minecraft:stone_ore_replaceables', 'my_mod:blockium')
    })
    ```

You can also add ores in other dimensions, but to do so you will have to create a custom World Generation Layer.    
You'll learn how to do so during the next few chapters.
