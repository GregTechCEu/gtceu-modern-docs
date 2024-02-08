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
