---
title: Ore Generation
---


# Ore Generation


## Adding a Custom Ore Vein

```js title="custom_vein.js"
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

```js title="ore_vein_removal.js"
GTCEuServerEvents.oreVeins(event => {
     event.remove("gtceu:magnetite_over_vein") 
})
```


??? example "Removing all ore veins"
    If you want to remove **all** predefined ore veins (for example if you want to completely change ore generation
    in your modpack), you can use the following code:

    ```js
    GTCEuServerEvents.oreVeins(event => {
        GTRegistries.ORE_VEINS.keys().forEach(id => event.remove(id))
    })
    ```


## Modifying Contents of an Existing Vein

```js title="ore_vein_modify_contents.js"
const $Either = Java.loadClass("com.mojang.datafixers.util.Either")
GTCEuServerEvents.oreVeins(event => {
    event.modify("gtceu:cassiterite_vein", vein => {
        vein.veinGenerator.layerPatterns.get(0).layers.get(0).targets.set(0, $Either.right(GTMaterials.get('diamond')))
    })//(1)
})
```

1. This currently doesn't work due to a bug present in Rhino.


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
   _See [Creating a New World Gen Layer](#creating-a-new-world-gen-layer)_


## Creating a New World Gen Layer

```js title="world_gen_layers.js"
GTCEuStartupEvents.registry('gtceu:world_gen_layer', event => {
    event.create('air')
        .target([])
})
```