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
        vein.clusterSize(40)
        vein.weight(200)
        vein.layer("deepslate")
        vein.density(0.25)

        vein.addSpawnDimension("minecraft:overworld")
        vein.addSpawnBiome("#minecraft:is_overworld")

        vein.heightRange({
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
        vein.discardChanceOnAirExposure(0)
        vein.generator({
            type: "gtceu:layer",
            layer_patterns: [
                [
                    {
                        targets: [
                            "gold",
                            "tricalcium_phosphate"
                        ],
                        min_size: 2,
                        max_size: 2,
                        weight: 3
                    },
                    {
                        targets: [
                            "copper",
                            "vanadium_magnetite"
                        ],
                        min_size: 1,
                        max_size: 3,
                        weight: 1
                    }
                ]
            ]
        })
    })
})
```


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
