---
date: 2021-02-04T20:24
tags: 
  - programming/analogy of code design/volatility decomposition
---

# Electricity is extreamly volatile

Implementing electricity as a feature to your system and considering the
volatilities of it by desigining by #[[volatility-decomposition]], then you'll
quickly notice that electricity is extreamly volatile.

## Volatilities of electricity

These are things that can change, and probably will change. You as a designer
need to account for these.

You'll have to pick your fights. What range of options do you want to support
per volatility?

- Power source

  - Wind mill
  - Generator
  - Solar panel
  - Geothermal

- Voltage

  - $230V$ (as per european customs)
  - $120V$ (as per american customs)

- Frequency

  - 50 Hz (as per european customs)
  - 60 Hz (as per american customs)

## Features of electricity

- Connecting power plug and equipment is powered.
- Electricute some organism.
- Ignite gas.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.

- Mains electricity. (2021, February 2). In *Wikipedia*.
  <https://en.wikipedia.org/wiki/Mains_electricity>
