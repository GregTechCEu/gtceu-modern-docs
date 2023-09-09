---
title: Element Creation
---

## Element Creation
```js
GTCEuStartupEvents.registry('gtceu:element', event => {
   event.create('test_element', 27, 177, -1, null, 'test', false) // (1)
})
```

1. Element Name, Protons, Neutrons, Half Life Seconds, Decay To, Atomic Symbol, Is Isotope
