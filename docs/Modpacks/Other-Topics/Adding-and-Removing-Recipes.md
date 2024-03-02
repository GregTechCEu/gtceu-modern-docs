---
title: "Adding & Removing Recipes"
---


# Adding and Removing Recipes

## Removing Recipes

Removing GTCEu Modern recipes with KubeJS works the same as any other recipe, meaning they can be removed by: ID, Mod, Input, Output, Type or a Mixture.

```js title="gtceu_removal.js"
ServerEvents.recipes(event => {
    event.remove({ id: 'gtceu:smelting/sticky_resin_from_slime' }) // (1)
    event.remove({ mod: 'gtceu' }) // (2)
    event.remove({ type: 'gtceu:arc_furnace' }) // (3)
    event.remove({ input: '#forge:ingots/iron' }) // (4)
    event.remove({ output: 'minecraft:cobblestone' }) // (5)
    event.remove({ type: 'gtceu:assembler', input: '#forge:plates/steel' }) // (6)
})
```

1. Targets the slime to sticky resin furnace recipe only for removal.
2. Targets all recipes under the gtceu mod id for removal.
3. Targets all recipes in the arc furnace for removal.
4. Targets all recipes that have an input of `#forge:ingots/iron` for removal.
5. Targets all recipes that have an output of `minecraft:cobblestone` for removal.
6. Targets all recipes in the gtceu assembler that have an input of `#forge:plates/steel` for removal.


## Modifiying Recipes

With KubeJS it is possible to modfiy the Inputs or Outputs of existing GTCEu Modern recipes, which uses the same method of targeting the recipes.

```js title="gtceu_modify.js"
ServerEvents.recipes(event => {
    event.replaceInput({ mod: 'gtceu' }, 'minecraft:sand', '#forge:sand') // (1)
    event.replaceOutput({ type: 'gtceu:arc_furnace' }, 'gtceu:wrought_iron_ingot', 'minecraft:dirt') // (2)
})
```

1. Targets all gtceu recipes that have and input of `minecraft:sand` and replaces it with `#forge:sand`.
2. Targets all gtceu arc furnace recipes that have and output of `gtceu:wrought_iron_ingot` and replaces it with `minecraft:dirt`.


## Adding Recipes

Syntax: `event.recipes.gtceu.RECIPE_TYPE(string: recipe id)`

```js title="gtceu_add.js"
ServerEvents.recipes(event => {
    event.recipes.gtceu.assembler('test')
        .itemInputs(
            '64x minecraft:dirt',
            '32x minecraft:diamond'
        )
        .inputFluids(
            Fluid.of('minecraft:lava', 1500)
        )
        .itemOutputs(
            'minecraft:stick'
        )
        .duration(100)
        .EUt(30)
})
```

### Event Addons

- Inputs:
    - Items:
        - `.itemInput()`
        - `.itemInputs()`
        - `.chancedInput()`
        - `.notConsumable()`
    - Fluids:
        - `.inputFluids()`
        - `.chancedFluidInput()`
    - Misc:
        - `.circuit()`
- Outputs:
    - Items:
        - `.itemOutput()`
        - `.itemOutputs()`
        - `.chancedOutput()`
    - Fluids:
        - `.outputFluids`
        - `.chancedFluidOutput()`
- Energy:   
    
    

### Rhino Jank

!!! warning
    Due to some Rhino Jank, when adding rock breaker recipes you will need to manually tell Rhino how to interpret `.addData()`.

```js title="rhino_jank_rock_breaker.js"
ServerEvents.recipes(event => {
    const RockBreakerCondition = Java.loadClass("com.gregtechceu.gtceu.common.recipe.RockBreakerCondition")

    event.recipes.gtceu.rock_breaker('rhino_jank')
        .notConsumable('minecraft:dirt')
        .itemOutputs('minecraft:dirt')
        ["addData(java.lang.String,java.lang.String)"]("fluidA", "minecraft:lava")
        ["addData(java.lang.String,java.lang.String)"]("fluidB", "minecraft:water")
        .duration(16)
        .EUt(30)
        .addCondition(RockBreakerCondition.INSTANCE)
})
```
