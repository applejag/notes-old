---
date: 2021-01-30T16:00
tags:
  - stub
---

# Designing software vs hardware

Common argument for designing the architecture differently for software vs
hardware, such as using #[[functional-decomposition]] which is rarely ever used
in hardware architectures design procedures, is:

> Software is different than hardware. It's *soft*ware, i.e. it's easy to change
> so we don't have to be as careful when designing it.

That's the misconception though.

## Fewer limits $\nRightarrow$ easier

The "building a house" analogy is so easy to work with, so let's continue with
that topic.

In software, we don't have those limit factors that physics usually puts on us.
You can paint the walls before you actually built them.

Law of the [[allure-of-the-free-lunch]] still applies here, as well as all the
other design principles that engineers such as mechanical engineers have to
consider.

There's a huge freedom with software to be able to rip out dependency with such
a lower cost than ripping out a sink from a kitchen. Though this is still not
an argument for relying on these hotswapping capabilities.

With fewer limits comes greater responsabilties. More stuff that can go wrong.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
