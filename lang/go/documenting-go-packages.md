---
date: 2021-01-24T11:35
tags: 
  - go/best practices in golang
  - go/writing idiomatic golang code
  - go/create a lasting go project
  - programming/writing documentation
---

# Documenting Go packages

Documenting your Go packages, both libraries and main packages, is essential to
keeping yourself and your users well informed of how to use your package.

In contrast to C\#'s XML comments, Go documentation does not rely on any other
language than English and Go itself. It goes hand-in-hand with the
[G1: Multiple Languages in One Source File](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/general/g1-multiple-languages-in-one-source-file.html)
heuristic, as mentioned in Uncle Bob's book *"Clean Code"*.

## Package-level comment

Place this in `main.go`, `doc.go`, or any other obvious location. It should be
easy to find it. Common convention on projects with a lot of files is to place
it in `doc.go`.

```go
// My license.
// Can be multiline.

// Package mypkg is a sample package I use to demonstrate documentation in Go.
//
// It can also be multiline.
// It can also contain code blocks:
//
//      // though it needs to be indented
package mypkg
```

Or with block comments:

```go
// My license.
// Can use block comment as well, but it's less common.

/*
    Package mypkg is a sample package I use to demonstrate documentation in Go.

    It can be a block comment, but must be placed directly before the package
    declaration:

        // like this
        package mypkg
*/
package mypkg
```

- Start the package comment with `Package ${package-name} ...`.

- Use full sentences with proper capitalization and punctuation.

- Use indentation for code blocks.

- Concise first sentence that briefly but completely explain the purpose of the
  package.
  
- Package comment is only the comment(s) directly above the package declaration.
  If you leave a gap with an empty line that will omit the non-connected comment
  sections, such as with the licenses in the examples above.
  
## Member/types commenting

```go
// DefaultPort is the port used when no port has been specified through
// configurations.
const DefaultPort int = 8080

// Config is the configuration you pass to the TCP/IP server constructors.
type Config struct {
    Port int
}

// Stack represents a the stack data structure, with
// first-in-last-out/last-in-first-out element access.
type Stack interface {
    // Push will append the elem to the list at the top.
    Push(string)

    // Pop will remove the last inserted element from the top of the list and
    // return it; or return
    //
    //      ("", false)
    //
    // ...if the stack is empty.
    Pop() (string, bool)
}

// Push will append the elem to the list at the top.
func (s *[]string) Push(elem string) {
    // ...
}

// Pop will take the last inserted element from the top of the list and return
// it; or return
//
//      ("", false)
//
// ...if the stack is empty.
func (s *[]string) Pop() (string, bool) {
    // ...
}
```

- Start the member comment with `${Member-name} ...`. Sometimes starting with
  `The ${Member-name} ...` is used, but try to avoid it.

- Use full sentences with proper capitalization and punctuation.

- Focus on commenting public members, as only public members will get their
  comments exported by `go doc`. Private member documentation has its benefits,
  but is usually not as needed.

## References

- Mike Van Sickle. (2019, July 29). *Deep Dive into Go Packages* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-packages-deep-dive>

- Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*
  (1st ed.). Pearson.
  
  - *Cited via* Metcalfe, D. (2019, January 22). *Clean Code: Smells and
    Heuristics.*
    <https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/>
