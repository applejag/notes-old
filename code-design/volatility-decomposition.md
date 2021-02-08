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

Primary goal: Encapsulate change.

## Surviving a hand-grenade of changes

Imagine your system. If you were to hand a live and fused grenade to one of its
components, what will happen to the rest of the system?

Given you've designed by [[functional-decomposition]], the result will most
probably be that the component explodes, and fragments of the explosion shatters
across the entire system, damaging seemingly unrelated components.

Now a perfectly designed system that was designed by volatility-based
decomposition can be compared to a set of vaults. You toss a grenade into one of
the vaults (components) and the component is destroyed, but the shrapnel is
contained by the walls of the vault.

The grenade in this case are *changes*.

This is what you want to achieve with volatility-based decomposition.
You want to **encapsulate change.**

[[z:zettels?tag=programming/analogy+of+code+design/volatility+decomposition]]

## Where to start

1. To start desiging, you must start with [[finding-a-systems-volatilities]]#.

2. Continue with [[finding-a-systems-components]]# based on the volatilities.

## Issues with volatility-based decomposition

There are plenty, and all originates from the fact that it's more difficult
and requires more sweating than [[functional-decomposition]].

[[z:zettels?tag=code+design/issues+with+volatility+decomposition]]

## Universal rule

One of the favorite aspects of volatility-based decomposition, according to
Juval Löwy, is that these rules and principles work universally when designing.

There's no small footnote specifying that this *"Does not apply to software"*
([[designing-software-vs-hardware]]).

Everything is designed through volatility decomposition, because while it's the
difficult route, it is also the only resilient one.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.

[^srp]: Martin, R. (2008). The Single Responsibility Principle. In *Clean Code: A Handbook of Agile Software Craftmanship* (*Robert C. Martin Series*) (1st ed., pp. 138-140). Pearson.
[^ccp]: Martin, R. (2017). The Common Closure Principle. In *Clean Architecture: A Craftsman’s Guide to Software Structure and Design* (*Robert C. Martin Series*) (1st ed., pp. 105–107). Pearson.
