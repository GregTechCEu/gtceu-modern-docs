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

## Material Flags
```js 
- GTMaterialFlags.BLAST_FURNACE_CALCITE_DOUBLE
- GTMaterialFlags.BLAST_FURNACE_CALCITE_TRIPLE
- GTMaterialFlags.CRYSTALLIZABLE
- GTMaterialFlags.DECOMPOSITION_BY_CENTRIFUGING
- GTMaterialFlags.DECOMPOSITION_BY_ELECTROLYZING
- GTMaterialFlags.DISABLE_DECOMPOSITION
- GTMaterialFlags.EXCLUDE_BLOCK_CRAFTING_BY_HAND_RECIPES
- GTMaterialFlags.EXCLUDE_BLOCK_CRAFTING_RECIPES
- GTMaterialFlags.EXCLUDE_PLATE_COMPRESSOR_RECIPES
- GTMaterialFlags.EXPLOSIVE
- GTMaterialFlags.FLAMMABLE
- GTMaterialFlags.FORCE_GENERATE_BLOCK
- GTMaterialFlags.GENERATE_BOLT_SCREW
- GTMaterialFlags.GENERATE_DENSE
- GTMaterialFlags.GENERATE_FINE_WIRE
- GTMaterialFlags.GENERATE_FOIL
- GTMaterialFlags.GENERATE_FRAME
- GTMaterialFlags.GENERATE_GEAR
- GTMaterialFlags.GENERATE_LENS
- GTMaterialFlags.GENERATE_LONG_ROD
- GTMaterialFlags.GENERATE_PLATE
- GTMaterialFlags.GENERATE_RING
- GTMaterialFlags.GENERATE_ROD
- GTMaterialFlags.GENERATE_ROTOR
- GTMaterialFlags.GENERATE_ROUND
- GTMaterialFlags.GENERATE_SMALL_GEAR
- GTMaterialFlags.GENERATE_SPRING
- GTMaterialFlags.GENERATE_SPRING_SMALL
- GTMaterialFlags.HIGH_SIFTER_OUTPUT
- GTMaterialFlags.IS_MAGNETIC
- GTMaterialFlags.MORTAR_GRINDABLE
- GTMaterialFlags.NO_SMASHING
- GTMaterialFlags.NO_SMELTING
- GTMaterialFlags.NO_UNIFICATION
- GTMaterialFlags.NO_WORKING
- GTMaterialFlags.SOLDER_MATERIAL
- GTMaterialFlags.SOLDER_MATERIAL_BAD
- GTMaterialFlags.SOLDER_MATERIAL_GOOD
- GTMaterialFlags.STICKY
```

## Icon Sets

```js 
- GTMaterialIconSet.BRIGHT
- GTMaterialIconSet.CERTUS
- GTMaterialIconSet.DIAMOND
- GTMaterialIconSet.DULL
- GTMaterialIconSet.EMERALD
- GTMaterialIconSet.FINE
- GTMaterialIconSet.FLINT
- GTMaterialIconSet.FLUID
- GTMaterialIconSet.GAS
- GTMaterialIconSet.GEM_HORIZONTAL
- GTMaterialIconSet.GEM_VERTICAL
- GTMaterialIconSet.GLASS
- GTMaterialIconSet.LAPIS
- GTMaterialIconSet.LIGNITE
- GTMaterialIconSet.MAGNETIC
- GTMaterialIconSet.METALLIC
- GTMaterialIconSet.NETHERSTAR
- GTMaterialIconSet.OPAL
- GTMaterialIconSet.QUARTZ
- GTMaterialIconSet.ROUGH
- GTMaterialIconSet.RUBY
- GTMaterialIconSet.SAND
- GTMaterialIconSet.SHINY
- GTMaterialIconSet.WOOD
- GTMatericalIconset.get('') // (1)
```

1. Used for specifying custom iconsets, for example `GTMatericalIconset.get('infinity')`.

## Properties (WIP)
```js
- BlastProperty:
   - .blastTemp() // (1)
   - .gasTier() // (2)
   - .durationOverride() // (3)
   - .eutOverride() // (4)
- DustProperty:
   - .dust() // (5)
- FluidPipeProperty:
   - .fluidPipeProperties() // (6)
- FluidProperty:
   - .fluid() // (7)
   - .isGas() // (8)
   - .hasBlock() 
- GemProperty:
   - .gem()
- IngotProperty:
   - .ingot() // (9)
      - .smeltInto()
      - .arcSmeltInto()
      - .magneticMaterial()
      - .macerateInto()
- OreProperty:
   - .ore() // (10)
```

1. Sets the Blast Furnace Temperature of the material. If the temperature is below 1000K recipes will be generated in the Primitive Blast Furnace. If above 1750K recipes for the Hot Ingot will be created along with the Vacuum Freezer Recipe to cool the ingot. Example: `.blastTemp(2750)`

2. Sets the Gas Tier which determins what GAS EBF recipes will be generated. Example: `.gasTier(LOW)`

3. Overrides the EBF's default behaviour for recipe durations.

4. Overrides the EBF's default behaviour for EU/t.

5. Used for creating a dust material. The haverst level and burn time can be specified in the brackets. Example: `.dust(2, 4000)`

6. Creates a fluid pipe out of the material it is added to. The possible values are: Max Fluid Temperature, Throughput, Gas Proof, Acid Proof, Cyro Proof, Plasma Proof,
 Channels. Example: `.fluidPipeProperties(9620, 850, false, false, false, false, 1)`
