---
title: Material Creation
---


## Creating an Ingot

```js title="ingot.js"
GTCEuStartupEvents.registry('gtceu:material', event => {
    event.create('andesite_alloy')
        .ingot()
        .components('1x andesite', '1x iron')
        .color(0x839689).iconSet(GTMaterialIconSet.DULL)
        .flags(GTMaterialFlags.GENERATE_PLATE, GTMaterialFlags.GENERATE_GEAR, GTMaterialFlags.GENERATE_SMALL_GEAR)
})
```


## Creating a Gem

```js title="gem.js"
GTCEuStartupEvents.registry('gtceu:material', event => {
    event.create('purple_coal')
        .gem(2, 4000) 
        .element(GTElements.C) 
        .ore(2, 3) 
        .color(0x7D2DDB).iconSet(GTMaterialIconSet.LIGNITE)
})
```


## Creating a Dust

```js title="dust.js"
GTCEuStartupEvents.registry('gtceu:material', event => {
    event.create('mysterious_dust')
        .dust()
        .cableProperties(GTValues.V[GTValues.LV], 69, 0, true) // (1)
})
```

1. Voltage, Amperage, EU loss, Is Superconductor.


## Creating a Fluid

```js title="fluid.js"
GTCEuStartupEvents.registry('gtceu:material', event => {
    event.create('mysterious_ooze')
        .fluid()
        .color(0x500bbf)
        .fluidTemp(69420) 
})
```
