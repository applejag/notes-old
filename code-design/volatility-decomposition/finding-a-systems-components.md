---
date: 2021-02-08T20:55
tags: 
  - code design/how to do volatility decomposition
---

# Finding a system's components

Before you seek to define the components of a system, you first need to
be #[[finding-a-systems-volatilities]].

## Designing components

Each volatility can be seen as an "area of change". This goes hand in hand with
the *Single Responsibility Principle (SRP)[^srp]* or the *Common Closure
Principle (CCP)[^ccp]*, that specifies that a component should not be bloated
with responsabilities to make changes more intact.

To clarify:

- Each component should be based on 1 (one) *area of change*, and not by a set of
  features.
  
- Each volatility does not need its own component.

- A good design has a low amount of frivolous components, as well as clear
  boundaries between its *areas of change*.

The [[volatilities-and-components-of-pumping-blood]]# analogy describes this
difference more concretely.

## Song of the siren

TODO

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.

[^srp]: Martin, R. (2008). The Single Responsibility Principle. In *Clean Code: A Handbook of Agile Software Craftmanship* (*Robert C. Martin Series*) (1st ed., pp. 138-140). Pearson.
[^ccp]: Martin, R. (2017). The Common Closure Principle. In *Clean Architecture: A Craftsman’s Guide to Software Structure and Design* (*Robert C. Martin Series*) (1st ed., pp. 105–107). Pearson.
