---
title: "Layers & Dimensions"
---


# Layers and Dimensions


## Creating a New World Gen Layer

```js title="world_gen_layers.js"
GTCEuStartupEvents.registry('gtceu:world_gen_layer', event => {
    event.create('air')
        .target([])
})
```