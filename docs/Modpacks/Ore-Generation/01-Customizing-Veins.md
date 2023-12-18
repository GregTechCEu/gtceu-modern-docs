---
title: "Customizing Veins"
---


# Creating and Modifying Ore Veins

You can create your own custom ore veins using KJS.  
It is also possible to modify or even delete existing ones.


## Creating New Veins

```js title="server_scripts/custom_ore_vein.js"
GTCEuServerEvents.oreVeins(event => {
    event.add("kubejs:custom_vein", vein => {
        // Basic vein generation properties
        vein.weight(200) // [*] (1)
        vein.clusterSize(40) // [*] (2)
        vein.density(0.25) // [*] (3)
        vein.discardChanceOnAirExposure(0) // (4)

        // Define where the vein can generate
        vein.layer("deepslate") // [*] (5)
        vein.dimensions("minecraft:overworld") // (6)
        vein.biome("#minecraft:is_overworld") // (7)

        // Define a height range:
        // You must choose EXACTLY ONE of these options! [*]
        vein.heightRangeUniform(-60, 20) // (8)
        vein.heightRangeTriangle(-60, 20) // (9)
        vein.heightRange(/* ... */) // (10)

        // Define the vein's generator:
        vein.generator(/* ... */) // [*] (11)

        // Add one or more type of surface indicator to the vein:
        vein.addIndicator(/* ... */) // (12)
    })
})
```

1. An ore vein's weight determines the chance of it being chosen over another vein type, to be generated at a possible vein location.  
   The higher the weight, the more frequently an ore vein type will be generated.
2. Cluster size determines the diameter of an ore vein.
3. The density determines how frequently ores occur inside the vein.
4. Determines the chance of an ore block being skipped when it is exposed to air. Must be between `0` and `1`.  
   **Default:** `0`
5. See [Layers & Dimensions](./04-Layers-and-Dimensions.md)
6. Limits vein generation to the supplied dimensions. Note that these vein's layer must be applicable for them.  
   **Default:** All dimensions of the vein's layer.  
   <br>
   _Accepts any number of parameters._
7. Determines the biome (or biome tag) the vein can generate in.  
   **Default:** If no biome is explicitly set, the vein will generate in any biome.  
   <br>
   _Accepts either a single biome tag (prefixed with `#`), or any number of individual biomes._
8. Uniformly distributed across the height range
9. Biased towards the center of the height range
10. You can also use Minecraft's `HeightRangePlacement` directly, instead of the above shorthand versions:  
    ```js
    vein.heightRange(
        height: {
            type: "uniform",
            min_inclusive: {
                absolute: -60
            },
            max_inclusive: {
                absolute: 20
            }
        }
    })
    ```
11. See [Generators](./02-Generators.md#vein-generators) for a list of available generators.
12. See [Generators](./02-Generators.md#indicator-generators) for a list of available generators.


??? example "Creating a new biome tag for your ore vein"
    In case you want to limit your ore vein to multiple biomes that don't have a common tag yet, you need to add one first:

    ```js title="server_scripts/biome_tags.js"
    ServerEvents.tags('biome', event => {
        event.add('kubejs:my_biome_tag', 'minecraft:forest')
        event.add('kubejs:my_biome_tag', 'minecraft:river')
    })
    ```

    You can then use your biome tag by simply calling `vein.biome('#kubejs:my_biome_tag')` in your vein definition.


## Removing an Existing Ore Vein

```js title="server_scripts/remove_ore_vein.js"
GTCEuServerEvents.oreVeins(event => {
     event.remove("gtceu:magnetite_over_vein") 
})
```


??? example "Removing all ore veins"
    If you want to remove **all** predefined ore veins (for example if you want to completely change ore generation
    in your modpack), you can use the following code:

    ```js
    GTCEuServerEvents.oreVeins(event => {
        let removed_veins = GTRegistries.ORE_VEINS.keys().stream().toList() // (1)
        removed_veins.forEach(id => event.remove(id))
    })
    ```

    1. Copying the keys first is necessary to avoid modifying the registry while iterating over it.


## Modifying Contents of an Existing Vein

!!! warning
    This currently doesn't work due to a bug.

```js title="modify_ore_vein.js"
const $Either = Java.loadClass("com.mojang.datafixers.util.Either")
GTCEuServerEvents.oreVeins(event => {
    event.modify("gtceu:cassiterite_vein", vein => {
        vein.veinGenerator.layerPatterns.get(0).layers.get(0).targets.set(0, $Either.right(GTMaterials.get('diamond')))
    })
})
```


## Modifying Ore Veins To Generate In Additional World Gen Layers

```js title="ore_vein_modify_worl_gen_layers.js"
const $GTOreFeatureEntry = Java.loadClass('com.gregtechceu.gtceu.api.data.worldgen.GTOreFeatureEntry')

GTCEuServerEvents.oreVeins(event => {
    $GTOreFeatureEntry.ALL.keySet().forEach(veinId => {
        event.modify(veinId, vein => {
            vein.layer('air')
        })
    }) //(1)
})
```

1. For this to work you must first create the new world gen layer of `air`.  
   _See [Creating a New World Gen Layer](./03-Layers-and-Dimensions.md#creating-a-new-world-gen-layer)_
