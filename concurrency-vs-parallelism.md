---
date: 2021-01-30T13:02
tags: 
  - programming/supporting concurrency
---

# Concurrency vs parallelism

The two terms are commonly used interchangeably, and most times it seems as they
can be.

But they have two different definitions, and when you talk about supporting
concurrency or supporting parallelism you're talking about two distinct tasks.

## Concurrency

The capability of interchanging multiple different tasks.

Such as when you're shopping you can at any time swap between looking for apples
or looking for bread. A shoppinglist is inheritly a concurrent list of tasks.

Allowing concurrency means you allow switching tasks at any point.

## Parallelism

Doing multiple things at the same time, simontaneously. This depends on the fact
that the tasks support concurrency.

Such as when you're shopping with friends. You can give each friend a section of
the shopping list, and all items on the list will be retrieved in parallel.

Allowing parallelism means you allow multiple tasks to be worked on
simontaneously.

## References

- Mike Van Sickle. (2015, June 5). *Concurrent Programming with Go* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-concurrent-programming>
