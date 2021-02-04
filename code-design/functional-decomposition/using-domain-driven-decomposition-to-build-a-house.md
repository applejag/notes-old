---
date: 2021-01-28T20:01
tags: 
  - programming/why functional decomposition is bad
  - programming/incorrectly designing a house
  - programming/designing hardware as if it was software
  - programming/analogy of code design/functional decomposition
---

# Using domain-driven decomposition to build a house

To build a house, you could be [[using-functional-decomposition-to-build-a-house]]
by finding the requirements and adding features to meet those current
requirements.

But that seems quite narrow and easy to break. A common counter that the software
world mentions is to instead look into domain-driven decomposition (often
referred to as *"Domain Driven Design"*, or *"DDD"*).

This however, is no different than saying you're using [[functional-decomposition]]
to build a house. You're just expanding the scope of the features.

> "[Domain-driven decomposition] is still death [to a project], but in disguise."
>
> - J. Löwy (January 27, 2021)

But let's consider the scenario of building a house, using DDD.

## Identify the domains

- Kitchen
- Garage
- Bedroom 1
- Bedroom 2
- Living room
- Attic
- Restroom

## Start implementing 

You build up the beedrooms, the kitchen, the garage, all with their own
responsibilities. This works fine.

## Requirements change

Your client wants to eat dinner in bedroom 1. You did not antisipate this, and
now you need to take some of the "eating" functionality from "living room" and
spray it over bedroom.

There, now your client can eat while in bed.

But then they want to have a snack in the garage, or let the kids and their
friends have a small picknic in the attic.

How about if your client wants to have a friend over and wants to use the living
room for their guest to sleep in?

Your system explodes with duplicated features all over.

## A real house

We've all been in a real house. If our desks were designed to solely conform the
features of holding up pens, notebooks, and monitors, then bringing a plate of
food onto it would just result in the plate falling off, the plate would shatter,
or even the desk would collapse.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
