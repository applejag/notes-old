---
date: 2021-01-30T13:01
tags: 
  - go/best practices in golang
  - go/writing idiomatic golang code
---

# Parallelism in Go

Writing #[[go]] code that runs in parallel first requires your use case to support
concurrent tasks. (#[[concurrency-vs-parallelism]])

You OS has a native support for threads. Most programming languages however
supply some kind of abstraction on top of threads though as thread have quite the
big amount of overhead. Go is no different.

In Go, to make some of your code run in parallell, you need to use so called
*goroutines*.

## Threads vs Goroutines

| Abstraction | Starting memory allocation | Memory can grow? |
| ----------- | -------------------------- | ---------------- |
| Thread      | ~1 MB                      | No.              |
| Goroutine   | ~2 kB                      | Yes.             |

Goroutines still has a little bit of overhead for each goroutine you create, but
as the initial memory allocation (for their stack) is so low you as a user can
approximately start up ~500 times more goroutines than threads on your computer,
leading to being able to instantiate up to millions of goroutines.

There's no way to cheat the limit of number of CPU's, so you can't have
million of goroutines running in complete parallelism, but Go deals with the
concurrency and goroutine-switching for you so all your different goroutines get
all to execute.

[[z:zettels?tag=go/concurrent+programming]]#

## References

- Mike Van Sickle. (2015, June 5). *Concurrent Programming with Go* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-concurrent-programming>
