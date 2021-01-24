---
date: 2021-01-24T14:33
tags: 
  - go/best practices in golang
  - go/writing idiomatic golang code
  - go/using packages in go
---

# Ways of importing Go packages

There are lots of ways to import packages in Go. Some syntactic difference but
semantically identical, and some minor syntactic differences but with huge
impact on the import's meaning.

## Package name

You use a package depending on its package name. Usually, the name of a repo
strongly reflects its package name.

```go
// From repo "github.com/someuser/somepkg"
package somepkg
func DoSomething() {
    // ...
}

// When using the package in some other repo
import "github.com/someuser/somepkg"
somepkg.DoSomething()
```

The name specified by the `package somepkg` statement declares what the imported
prefix will be set to. As an extreme sample, this is what you could do:

```go
// From repo "github.com/someuser/somepkg"
package foobar
func DoSomething() {
    // ...
}

// When using the package in some other repo
import "github.com/someuser/somepkg"
foobar.DoSomething()
```

It's common for developers to name their repo `go-something`, and have the
`package` statement just be `package something`.

## Importing a single package

```go
// Useful style when there's only 1 pkg
import "github.com/someuser/somepkg"

somepkg.DoSomething()

// This is OK as well, but above is preferred if there's only 1 pkg
import (
    "github.com/someuser/somepkg"
)
```

## Importing multiple packages

```go
// This is bad:
import "github.com/someuser/somepkg1"
import "github.com/someuser/somepkg2"


// This is good:
// Useful style when there's more than 1 pkg to import
import (
    "github.com/someuser/somepkg1"
    "github.com/someuser/somepkg2"
)
```

## Aliasing package names

```go
// From repo "github.com/someuser/json"
package json
func DoSomething() {
    // ...
}

// When using the package in some other repo
import (
    "encoding/json"
    // will collide with above json pkg name, so we rename/alias it
    somejson "github.com/someuser/json"
)

somejson.DoSomething()

// Alternatively aliasing with only 1 pkg
import somejson "github.com/someuser/json"
```

## Only import side-effects

```go
// From repo "github.com/someuser/somepkg"
package somepkg
func init() {
    // ...
}
func DoSomething() {
    // ...
}

// When using the package in some other repo
import (
    _ "github.com/someuser/somepkg"
)

// This will error:
somepkg.DoSomething()
```

## Import all members globally

```go
// From repo "github.com/someuser/somepkg"
package somepkg
func DoSomething() {
    // ...
}

// When using the package in some other repo
import (
    . "github.com/someuser/somepkg"
)

// No need for "somepkg."
DoSomething()
```

## Relative imports

> **Note:** This is deprecated and should not be used by any package! Support for
> this will eventually be removed, in favor of gomodules.

This requires a package to use vendoring instead of modules.

```go
import (
    "../../some/other/dir/branch"
    "./some/sub/dir"
)
```

## References

- Mike Van Sickle. (2019, July 29). *Deep Dive into Go Packages* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-packages-deep-dive>
