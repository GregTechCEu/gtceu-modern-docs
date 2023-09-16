---
title: "Greenhouse"
---


# Greenhouse Multiblock By: Drack.ion


## Recipe Type

```js title="greenhouse_recipe_type.js"
GTCEuStartupEvents.registry('gtceu:recipe_type', event => {
    event.create('greenhouse')
        .category('drack')
        .setEUIO('in')
        .setMaxIOSize(3, 4, 1, 0)
        .setProgressBar(GuiTextures.PROGRESS_BAR_ARROW, FillDirection.LEFT_TO_RIGHT)
        .setSound(GTSoundEntries.BATH)
})
```


## Multiblock

```js title="greenhouse_multiblock.js"
GTCEuStartupEvents.registry('gtceu:machine', event => {
    event.create('greenhouse', 'multiblock')
        .rotationState(RotationState.NON_Y_AXIS)
        .recipeType('greenhouse')
        .appearanceBlock(GTBlocks.CASING_STEEL_SOLID)
		.pattern(definition => FactoryBlockPattern.start()
			.aisle('CCC', 'CGC', 'CGC', 'CLC', 'CCC')
			.aisle('CMC', 'GSG', 'G#G', 'LIL', 'COC')
			.aisle('CKC', 'CGC', 'CGC', 'CLC', 'CNC')
			.where('K', Predicates.controller(Predicates.blocks(definition.get())))
			.where('M', Predicates.blocks('moss_block')
                .or(Predicates.blocks('dirt'))
                .or(Predicates.blocks('grass_block')))
			.where('G', Predicates.blocks('ae2:quartz_glass'))
			.where('S', Predicates.blocks('oak_sapling')
                .or(Predicates.blocks('dark_oak_sapling'))
                .or(Predicates.blocks('spruce_sapling'))
                .or(Predicates.blocks('birch_sapling'))
                .or(Predicates.blocks('jungle_sapling'))
                .or(Predicates.blocks('acacia_sapling'))
                .or(Predicates.blocks('azalea'))
                .or(Predicates.blocks('flowering_azalea'))
                .or(Predicates.blocks('mangrove_propagule'))
                .or(Predicates.blocks('gtceu:rubber_sapling')))
			.where('I', Predicates.blocks('glowstone'))
			.where('L', Predicates.blocks(GTBlocks.CASING_GRATE.get()))
			.where('C', Predicates.blocks(GTBlocks.CASING_STEEL_SOLID.get())
				.or(Predicates.autoAbilities(definition.getRecipeType())))
			.where('O', Predicates.abilities(PartAbility.MUFFLER).setExactLimit(1))
            .where('N', Predicates.abilities(PartAbility.MAINTENANCE))
			.where('#', Predicates.air())
            .build())
            .workableCasingRenderer('gtceu:block/casings/solid/machine_casing_solid_steel', 'gtceu:block/multiblock/implosion_compressor', false)
})
```


## Lang

```json title="en_us.json"
{
    "block.gtceu.greenhouse": "Greenhouse",
    "gtceu.greenhouse": "Greenhouse"
}
```


## Recipes

```js title="greenhouse_recipes.js"
ServerEvents.recipes(event => {
    //Machine Recipe
    event.shaped('gtceu:greenhouse', 
        ['AWA', 'CSC', 'WCW'], 
        {
            A: '#forge:circuits/mv', 
            W: 'gtceu:copper_single_cable',
            C: '#forge:circuits/mv',
            S: 'gtceu:solid_machine_casing'
        }).id('gtceu:shaped/greenhouse')
    //Tree Recipes
    function GHTree(sapling, log, sap, id, boosted, boosted_rubber, rubber) {
		if (boosted) {
			event.recipes.gtceu.greenhouse(`gtceu:${id}_sapling_boosted`)
				.circuit(2)
				.notConsumable(InputItem.of(sapling))
				.itemInputs('4x gtceu:fertilizer')
				.inputFluids(Fluid.of('minecraft:water', 1000))
				.itemOutputs(log, log, sap)
				.duration(320)
				.EUt(48)
		} else if (boosted_rubber) {
			event.recipes.gtceu.greenhouse(`gtceu:rubber_sapling_boosted`)
				.circuit(2)
				.notConsumable(InputItem.of('gtceu:rubber_sapling'))
				.itemInputs('4x gtceu:fertilizer')
				.inputFluids(Fluid.of('minecraft:water', 1000))
				.itemOutputs('64x gtceu:rubber_log', '16x gtceu:sticky_resin', '4x gtceu:rubber_sapling')
				.duration(320)
				.EUt(48)
		} else if (rubber) {
			event.recipes.gtceu.greenhouse(`gtceu:ruber_sapling`)
				.circuit(1)
				.chance(0)
				.notConsumable(InputItem.of('gtceu:rubber_sapling'))
				.chance(1)
				.inputFluids(Fluid.of('minecraft:water', 1000))
				.itemOutputs('32x gtceu:rubber_log', '8x gtceu:sticky_resin', '4x gtceu:rubber_sapling')
				.duration(640)
				.EUt(48)
		} else {
			event.recipes.gtceu.greenhouse(`gtceu:${id}_sapling`)
				.circuit(1)
				.notConsumable(InputItem.of(sapling))
				.inputFluids(Fluid.of('minecraft:water', 1000))
				.itemOutputs(log, sap)
				.duration(640)
				.EUt(48)
		}
	}
	//Rubber
		GHTree(null, null, null, null, false, false, true)
		GHTree(null, null, null, null, false, true, false)
	//Oak
		GHTree('minecraft:oak_sapling', '64x minecraft:oak_log', '4x minecraft:oak_sapling', 'oak', false, false, false)
		GHTree('minecraft:oak_sapling', '64x minecraft:oak_log', '4x minecraft:oak_sapling', 'oak', true, false, false)
	//Dark Oak
		GHTree('minecraft:dark_oak_sapling', '64x minecraft:dark_oak_log', '4x minecraft:dark_oak_sapling', 'dark_oak', false, false, false)
		GHTree('minecraft:dark_oak_sapling', '64x minecraft:dark_oak_log', '4x minecraft:dark_oak_sapling', 'dark_oak', true, false, false)
	//Spruce
		GHTree('minecraft:spruce_sapling', '64x minecraft:spruce_log', '4x minecraft:spruce_sapling', 'spruce', false, false, false)
		GHTree('minecraft:spruce_sapling', '64x minecraft:spruce_log', '4x minecraft:spruce_sapling', 'spruce', true, false, false)
	//Birch
		GHTree('minecraft:birch_sapling', '64x minecraft:birch_log', '4x minecraft:birch_sapling', 'birch', false, false, false)
		GHTree('minecraft:birch_sapling', '64x minecraft:birch_log', '4x minecraft:birch_sapling', 'birch', true, false, false)
	//Acacia
		GHTree('minecraft:acacia_sapling', '64x minecraft:acacia_log', '4x minecraft:acacia_sapling', 'acacia', false, false, false)
		GHTree('minecraft:acacia_sapling', '64x minecraft:acacia_log', '4x minecraft:acacia_sapling', 'acacia', true, false, false)
	//Jungle
		GHTree('minecraft:jungle_sapling', '64x minecraft:jungle_log', '4x minecraft:jungle_sapling', 'jungle', false, false, false)
		GHTree('minecraft:jungle_sapling', '64x minecraft:jungle_log', '4x minecraft:jungle_sapling', 'jungle', true, false, false)
	//Azalea
		GHTree('minecraft:azalea', '64x minecraft:oak_log', '4x minecraft:azalea', 'azalea', false, false, false)
		GHTree('minecraft:azalea', '64x minecraft:oak_log', '4x minecraft:azalea', 'azalea', true, false, false)
	//Flowering Azalea
		GHTree('minecraft:flowering_azalea', '64x minecraft:oak_log', '4x minecraft:flowering_azalea', 'flowering_azalea', false, false, false)
		GHTree('minecraft:flowering_azalea', '64x minecraft:oak_log', '4x minecraft:flowering_azalea', 'flowering_azalea', true, false, false)
	//Mangrove
		GHTree('minecraft:mangrove_propagule', '64x minecraft:mangrove_log', '4x minecraft:mangrove_propagule', 'mangrove', false, false, false)
		GHTree('minecraft:mangrove_propagule', '64x minecraft:mangrove_log', '4x minecraft:mangrove_propagule', 'mangrove', true, false, false)

    //Crop Recipes
    function GHPlant(seed, crop, water, id, boosted) {
		if (boosted) {
			event.recipes.gtceu.greenhouse(`gregicskies:${id}_boosted`)
				.circuit(2)
				.notConsumable(InputItem.of(seed))
				.itemInputs('4x gtceu:fertilizer')
				.inputFluids(Fluid.of('minecraft:water', water))
				.itemOutputs(crop)
				.duration(320)
				.EUt(48)
		} else {
			event.recipes.gtceu.greenhouse(`gregicskies:${id}`)
				.circuit(1)
				.notConsumable(InputItem.of(seed))
				.inputFluids(Fluid.of('minecraft:water', water))
				.itemOutputs(crop)
				.duration(320)
				.EUt(48)
		}
	}
	//Sugarcane
		GHPlant('minecraft:sugar_cane', '48x minecraft:sugar_cane', 1500, 'sugar_cane', true)
		GHPlant('minecraft:sugar_cane', '24x minecraft:sugar_cane', 1500, 'sugar_cane', false)
	//Kelp
		GHPlant('minecraft:kelp', '48x minecraft:kelp', 2000, 'kelp', true)
		GHPlant('minecraft:kelp', '24x minecraft:kelp', 2000, 'kelp', false)
	//Bamboo
		GHPlant('minecraft:bamboo', '48x minecraft:bamboo', 1000, 'bamboo', true)
		GHPlant('minecraft:bamboo', '24x minecraft:bamboo', 1000, 'bamboo', false)
	//Cactus
		GHPlant('minecraft:cactus', '48x minecraft:cactus', 1000, 'cactus', true)
		GHPlant('minecraft:cactus', '24x minecraft:cactus', 1000, 'cactus', false)
	//Wheat
		GHPlant('minecraft:wheat_seeds', '48x minecraft:wheat', 1000, 'wheat', true)
		GHPlant('minecraft:wheat_seeds', '24x minecraft:wheat', 1000, 'wheat', false)
	//Carrot
		GHPlant('minecraft:carrot', '48x minecraft:carrot', 1000, 'carrot', true)
		GHPlant('minecraft:carrot', '24x minecraft:carrot', 1000, 'carrot', false)
	//Potato
		GHPlant('minecraft:potato', '48x minecraft:potato', 1000, 'potato', true)
		GHPlant('minecraft:potato', '24x minecraft:potato', 1000, 'potato', false)
	//Beetroot
		GHPlant('minecraft:beetroot_seeds', '48x minecraft:beetroot', 1000, 'beetroot', true)
		GHPlant('minecraft:beetroot_seeds', '24x minecraft:beetroot', 1000, 'beetroot', false)
	//Melon
		GHPlant('minecraft:melon_seeds', '24x minecraft:melon', 1000, 'melon', true)
		GHPlant('minecraft:melon_seeds', '12x minecraft:melon', 1000, 'melon', false)
	//Pumpkin
		GHPlant('minecraft:pumpkin_seeds', '24x minecraft:pumpkin', 1000, 'pumpkin', true)
		GHPlant('minecraft:pumpkin_seeds', '12x minecraft:pumpkin', 1000, 'pumpkin', false)
	//Netherwart
		GHPlant('minecraft:nether_wart', '24x minecraft:nether_wart', 1000, 'nether_wart', true)
		GHPlant('minecraft:nether_wart', '12x minecraft:nether_wart', 1000, 'nether_wart', false)
	//Red Mushroom
		GHPlant('minecraft:red_mushroom', '24x minecraft:red_mushroom', 1000, 'red_mushroom', true)
		GHPlant('minecraft:red_mushroom', '12x minecraft:red_mushroom', 1000, 'red_mushroom', false)
	//Brown Mushroom
		GHPlant('minecraft:brown_mushroom', '24x minecraft:brown_mushroom', 1000, 'brown_mushroom', true)
		GHPlant('minecraft:brown_mushroom', '12x minecraft:brown_mushroom', 1000, 'brown_mushroom', false)
})
```