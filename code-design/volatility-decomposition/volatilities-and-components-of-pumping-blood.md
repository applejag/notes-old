---
date: 2021-02-04T20:36
tags: 
  - programming/analogy of code design/volatility decomposition
---

# Volatilities and components of pumping blood

Your veins. Anthropology. That kind of blood pumping.

This is an example to emphasize the difference between volatilities and
components when designing by #[[volatility-decomposition]].

## Volatilities

- Rate (frequency of blood pumped)

- Reactive to amount of oxygen consumed
  - Low rate when sleeping
  - High rate when running

- Pressure of blood

- Tempature of body

- Tempature
  - ...of body
  - ...of external, ex cold/hot weather

## Components

- Heart.

The heart is the sole component for dealing with the pumping of blood, yet it
deals with the above volatilities. In technical terms, it would be an *engine*.

The volatilities all form a single *area of change*. There's only one reason to
change the heart, and that would be if you needed to change the way blood is
pumped.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
