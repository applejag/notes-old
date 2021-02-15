---
date: 2021-02-15T18:59
tags: 
  - code design/how to do volatility decomposition
---

# Finding the nature of your buisness

What is the nature of your business? As in, what is the core use-case of your
system?

This question should be the first question to be answered when you want to design
a reliable and future-proof system. It is the first step when designing a system
using #[[volatility-decomposition]].

## They do not change

The core use-case of a system is the use-case that does not change.

While it technically can, it can also be considered near-infinitely unlikely, and
if the core use-case ever changes then it will do so in extreamly slow pace.

> *"Federal express is in the business of shipping packages. It could mean move
> into ballistic missile control, but not instantly and maybe never possible, but
> not plausible. And if possible, incredibly unlikely and very slowly."*
> --- J. Löwy, 42:00 (2020, April 24)

## Never encapsulate the nature of your business

Following [[volatility-decomposition]]#, you'll be encapsulating the different
areas of change. But given the above statement that the nature of your buisness
does not change, you're just encapsulating for no good reason.

This does not only create extra work and overhead, but this can actually hurt
your design.

If you design your system so that the core use-case can change, then arguably
your system does not have a core use case.

The core use-case helps you build your system in a rigid fashion to always
enhance it, and not change it.

Encapsulating the business needs can be considered the "Speculative design trap".

## Tips on identifying nature of your busniess

Look at your competitors and try identify the core use-cases for them.

Look at other projects, try to identify the core use-cases for them.

Even non-software projects.

Train yourself on identifying these things. Peaking at your competitors is the
easiest route, and is where you should look first.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.

- Doolittle, J. (Host). (2020, April 24). *Juval Löwy on Righting Software*
  (No. 407) [Audio podcast episode].
  In *Software Engineering Radio*. IEEE Software.
  <https://www.se-radio.net/2020/04/episode-407-juval-lowy-on-righting-software/>
