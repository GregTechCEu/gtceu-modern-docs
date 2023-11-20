---
title: Beyond the Docs
---


# Beyond the Docs

While we try to keep this documentation up to date and as complete as possible, it may not always contain all of the latest information.

As an additional resource to these docs, you can also reference our KubeJS integration directly in the source code:  
https://github.com/GregTechCEu/GregTech-Modern/tree/1.20.1/common/src/main/java/com/gregtechceu/gtceu/integration/kjs

Continue reading for a few important places you may want to check.


## Builders

!!! link "Builders"
    https://github.com/GregTechCEu/GregTech-Modern/tree/1.20.1/common/src/main/java/com/gregtechceu/gtceu/integration/kjs/builders

If you're not sure what methods and fields are available on one of our builders, you can find all of them in this directory.


## Bindings & Type Wrappers

!!! link "GregTechKubeJSPlugin"
    https://github.com/GregTechCEu/GregTech-Modern/blob/1.20.1/common/src/main/java/com/gregtechceu/gtceu/integration/kjs/GregTechKubeJSPlugin.java

- For a list of our custom bindings, see `GregTechKubeJSPlugin.registerBindings()`
- For a list of our type wrappers and their accepted inputs, see `GregTechKubeJSPlugin.registerTypeWrappers()`