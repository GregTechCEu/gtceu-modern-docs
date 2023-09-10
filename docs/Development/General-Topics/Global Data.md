---
title: Global Caches / Data
---


# Storing Data Globally

!!! warning inline end "Not yet merged<br>_Branch: `mi-ender-link`_"

In certain cases (e.g. in a cache that holds all currently loaded instances of a machine), you might need to store data
in a mutable static variable.  
When doing so, you need to ensure that clientside/remote and serverside instances don't get mixed up.