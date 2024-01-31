---
title: Bedrock Fluid Veins
---


Bedrock fluid veins can be pumped using fluid drills.

# Creating a Bedrock Fluid Vein


```js title="fluid_veins.js"
// In server events
GTCEuServerEvents.fluidVeins(event => {

    event.add('gtceu:custom_bedrock_fluid_vein', vein => {
        vein.addSpawnDimension('minecraft:overworld')
        vein.fluid(() => Fluid.of('gtceu:custom_fluid').fluid)
        vein.weight(600)
        vein.minimumYield(120)
        vein.maximumYield(720)
        vein.depletionAmount(2)
        vein.depletionChance(1)
        vein.depletedYield(50)
    });

```