---
date: 2021-01-28T20:00
tags: 
  - programming/how not to design software
dirtree:
  display: False
---

# Functional decomposition

Designing an architecture by inspecting the required functions. Functions comes
first in functional decomposition. This is discussed in [[juval-lowy]]'s
course on #[[righting-software]] about how **not** to design software.

It's the easiest way to build software and therefore also the most common, but
worse it's also partly why any other procedures is more or less unknown.

## Prevents reuse

This may seem contrary to what functional decomposition is actually meant to
solve. "By grouping each function, we split up the code and can reuse the
functions from the different services" *-said the naive architect.*

The problem lies in the integration. You implement the functions and start
adding integrations between them, thereby locking in the feature-sets. As a
result when you need to use a feature from one of the services, you either need
to add some bad spagetti integration between them or you duplicate the features.

Worst-, and most common case, is that some circular dependencies starts popping
up. When this happens the project could easily be declared dead, and any further
progress made on it will just keep on putting nails into the coffin of a rotten
corpse that is the project.

To strengthen the argument, we can look at:

- the comparison of [[designing-software-vs-hardware]]#,
- an example of [[stocks-trading-service-using-functional-decomposition]]#,
- or how using functional decomposition enforces [[locking-down-to-vendors]]#.

## Technical dept

There are many phrases to describe projects that are in bad shape.

- Code rot
- Technical dept

But they are all essentially the result of functional decomposition.

Due to functional decomposition, projects turn out so bad that the developers
say:

> We won't have it no more! We need to rebuild it

And then the manager does *not* (but should) answer:

> But you messed it up the last time...

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
