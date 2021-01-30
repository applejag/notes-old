---
date: 2021-01-24T14:14
tags: 
  - go/best practices in golang
  - go/writing idiomatic golang code
  - go/create a lasting go project
  - go/what is the internal folder in go projects
  - go/using packages in go
---

# Splitting up code into internal packages

To hide some of your internal logic in Go you can use private members.
But when you depend on too much internal logic, you face the difficulty of
sorting through tons of private methods that don't really have with one-another
to deal with.

What you can do is split up your Go package into multiple packages. Either you:

- make a sub-package, like how the [`net/http`](https://golang.org/src/net/http/)
  package depends on
  [`net/http/cookiejar`](https://golang.org/src/net/http/cookiejar/),
  
- or you make an internal package, like the
  [`net/http/internal`](https://golang.org/src/net/http/internal/) package.
  
Both options of splitting up the code base is to better conform with the *Single
Responsibility Principle (SRP)*, which is one of the key focus points in
[[what-to-focus-on-in-a-go-project]]#.

There's also multiple [[ways-of-importing-go-packages]]#, which is good to read up
on to take full advantage of both your internal packages, as well as any other
imported packages.

## Magic word: `internal`

Including the word `internal` in your package chain means it will be treated
differently by the Go compiler.

It's like a gate, where you can only access packages from the direct parents of
the internal package or sub-packages of an internal package.

Example:

```go
package github.com/myuser/mypkg/util/internal/stringhelper
```

The above package would be accessible by:

- ✔ `github.com/myuser/mypkg/util/internal/inthelper`
- ✔ `github.com/myuser/mypkg/util/internal/stringhelper/culture`
- ✔ `github.com/myuser/mypkg/util/internal`
- ✔ `github.com/myuser/mypkg/util`
- ✔ `github.com/myuser/mypkg`

But it would not be accessible by:

- ❌ `github.com/myuser/mypkg/cmd/mycmd`
- ❌ `github.com/myuser/mypkg/internal`
- ❌ `github.com/myuser/mypkg2`

## References

- Mike Van Sickle. (2019, July 29). *Deep Dive into Go Packages* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-packages-deep-dive>
