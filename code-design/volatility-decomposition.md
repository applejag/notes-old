---
date: 2021-01-28T20:00
tags: 
  - programming/how to design software
  - stub
dirtree:
  display: False
---

# Volatility decomposition

There are many ways to design software. According to the author #[[juval-lowy]],
using volatility-based decomposition is the perferred strategy, as he talks about
in his series of #[[righting-software]].

But make no misstake. This is no *"silver bullet"*. As Löwy puts it, *"You cannot
add value without sweating"* ([[allure-of-the-free-lunch]]#), and doing volatility
decomposition requires you to toil and *sweat* a lot.

## Surviving a hand-grenade

Imagine your system. If you were to hand a live and fused grenade to one of its
components, what will happen to the rest of the system?

Given you've designed by [[functional-decomposition]], the result will most
probably be that the component explodes, and fragments of the explosion shatters
across the entire system, damaging seemingly unrelated components.

Now a perfectly designed system that was designed by volatility-based
decomposition can be compared to a set of vaults. You toss a grenade into one of
the vaults (components) and the component is destroyed, but the shrapnel is
contained by the walls of the vault.

To repair, just get a new vault, and the issue is resolved.

This is what you want to achieve with volatility-based decomposition.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
