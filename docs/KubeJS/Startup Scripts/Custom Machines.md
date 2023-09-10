---
title: Custom Machines
---


## Creating Custom Steam Machine

```js title="test_steam_machine.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    event.create('test_simple_steam_machine', 'steam', true) // (1)
})
```

1. Machine ID, Machine Type, Has High Pressure Varient


## Creating Custom Electric Machine

```js title="test_electric_machine.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    event.create('test_electric', 'simple', GTValues.LV, GTValues.MV, GTValues.HV) // (1)
        .recipeType('test_recipe_type')
        .tankScalingFunction(tier => tier * 3200)
})
```

1. Machine ID, Machine Type, Voltage Tiers


## Creating Custom Kinetic Machine

```js title="test_kinetic_machine.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    
})
```


## Creating Custom Generator

```js
GTCEuStartupEvents.registry('gtceu:machine', event => {
    
})
```