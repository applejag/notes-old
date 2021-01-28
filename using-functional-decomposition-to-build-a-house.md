---
date: 2021-01-28T19:35
tags: 
  - programming/why functional decomposition is bad
  - programming/incorrectly designing a house
---

# Using functional decomposition to build a house

When designing software, #[[functional-decomposition]] is the most natural procedure.
It's the most common practice, because it's the easiest practice.

But it's terribly bad in the long run and results in software systems getting
remade instead of reused.

Here's an analogy of building a house using functional decomposition.

## Identify the functions

- Eating
- Sleeping
- Resting
- Learning
- Cooking
- Drinking
- Washing
- Bathing

## Start implementing cooking

We need to start somewhere. Let's start with cooking.

You imagine you start with a flat square of dirt and clear blue sky.

1. You place down a microwave on the ground.
2. Pull a cable from the nearest elecricity pole.
3. You start microwaving some food.

Done! Cooking fills its requirements!

## Requirements change

The customers actually wanted to be able to bake bread in their house.

No problem you add a small bench, place an oven on the ground, and call it a day.

## Nothing is build like this

This is madness. No house arcitect would simply start with the microwave. That's
a detail. You don't even start with the kitchen table. That's also a detail.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
