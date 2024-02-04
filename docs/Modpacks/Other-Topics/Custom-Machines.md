---
title: Custom Machines
---


# Custom Machines


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
        .rotationState(RotationState.NON_Y_AXIS)
        .recipeType('test_recipe_type')
        .tankScalingFunction(tier => tier * 3200)
})
```

1. Machine ID, Machine Type, Voltage Tiers


## Creating Custom Kinetic Machine

```js title="test_kinetic_machine.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    event.create('test_kinetic', 'kinetic', GTValues.LV, GTValues.MV, GTValues.HV)
        .rotationState(RotationState.NON_Y_AXIS)
        .recipeType('test_kinetic_recipe_type')
        .tankScalingFunction(tier => tier * 3200)
})
```


## Creating Custom Generator

```js title="test_generator.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    event.create('test_generator', 'generator', GTValues.LV, GTValues.MV, GTValues.HV) // (1)
        .recipeType('test_generator_recipe_type')
        .tankScalingFunction(tier => tier * 3200)
})
```


## Creating Custom Multiblock

```js title="test_multiblock.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    event.create('test_generator', 'multiblock')
        .rotationState(RotationState.NON_Y_AXIS)
        .appearanceBlock(GTBlocks.CASING_STEEL_SOLID)
        .recipeTypes(['test_recipe_type_1', 'test_recipe_type_2'])
        .pattern(definition => FactoryBlockPattern.start()
            .aisle('CCC', 'GGG', 'CCC')
            .aisle('CCC', 'GDG', 'CSC')
            .aisle('CKC', 'GGG', 'CMC')
            .where('K', Predicates.controller(Predicates.blocks(definition.get())))
            .where('M', Predicates.abilities(PartAbility.MAINTENANCE))
            .where('S', Predicates.abilities(PartAbility.MUFFLER))
            .where('D', Predicates.blocks(GTBlocks.COIL_CUPRONICKEL.get()))
            .where('G', Predicates.blocks('minecraft:glass'))
            .where('C', Predicates.blocks(GTBlocks.CASING_STEEL_SOLID.get())
                .or(Predicates.autoAbilities(definition.getRecipeTypes())))
        .build())
        .workableCasingRenderer(
            "gtceu:block/casings/solid/machine_casing_inert_ptfe",
            "gtceu:block/multiblock/large_chemical_reactor",
            false
        )
})
```