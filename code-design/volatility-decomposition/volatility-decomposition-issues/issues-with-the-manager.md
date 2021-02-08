---
date: 2021-02-08T19:38
tags: 
  - code design/issues with volatility decomposition
  - code design/what makes code design difficult
---

# Issues with the manager

Designing by #[[volatility-decomposition]] comes with its challenges. The greatest
of them all is dealing with the managers.

## Raging managers

> "WHY IS IT TAKING SO LONG TO ADVANCE???" --- *the manager*

Designing from volatility-based decomposition takes time. Much, much longer time
than #[[functional-decomposition]], especially when you start out.

By this reason, the managers will breathe down your neck, dubious to the work
you're putting into the design to make it *not* fail.

You will have to master volatility decomposition before you can try it out on
live projects, because the time limit will mean your manager will pull the plug
before the first line of code has already been written, or just let someone else
do the designing that they know can do it quicker.

**Managers will never understand.**

## Managers don't want the truth

The truth is that when managers tries to rush the design (as they've always
tried), which resulted in them getting the product quickly out the door (as
they've always wanted), they end up killing the project because it was
haphazardly put together (which they always are).

You cannot simply convince them *"just like that"*. Because of how it looks right
now, [[no-one-understands-they-are-killing-projects]], and no one would want to
receive nor accept that fact.

**Managers don't want to understand.**

## Dunning-Kruger effect

"Bias of unskilled people"

The managers will be the most unskilled people you will meet when it comes to
designing software. Therefore, they will assume it is easy, or that it can be
done quickly.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
