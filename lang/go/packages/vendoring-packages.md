---
date: 2021-01-24T14:53
tags: 
  - go/best practices in golang
  - go/writing idiomatic golang code
  - go/using packages in go
---

# Vendoring packages

This is an old way of resolving package that was used before Go invented so
called "gomodules".

If you're looking for how to import packages in your `.go` files, you should
instead read about [[ways-of-importing-go-packages]]#. This is about how different
versions of packages are referenced.

You can easily spot if a package uses the newer gomodules or the older vendoring
techniques by looking for:

- `vendor` directory &rarr; uses vendoring
- `go.mod`/`go.sum` files &rarr; uses gomodules

## Why was it needed?

Vendoring was invented by the community as a convention of how to deal with
packages with different versions.

For example, consider the following package dependency graph:

```
toppkg 1.0
  - utilpkg 2.0
  - webserver 1.0
    - httputil 2.3
      - utilpkg 1.0
```

The package `utilpkg` is referenced twice, and in the current state of the graph
it references two distinct major versions of that package. There could very well
have been some really backward incompatible changes between version 1.0 and 2.0.

The way Go resolved these packages *in the olden days* was to just use the
highest version available. This means that the above example dependency chain
might now compile because the way `toppkg` and `httputil` used `utilpkg` differed
too much when the `httputil` package all of the sudden has to compile against
`utilpkg` 2.0.

## Solution: Embed your dependencies

To solve this, the solution that appeared was to just embed the version you
depended on inside your own repository.

This was mainly done through either copy paste, or Git submodules.

When the Go compiler tries to fetch packages, it first checks if the given
package exists under `./vendor/${package-name}/`.

Example package structure:

```
/doc.go
/main.go
/vendor/github.com/someuser/utilpkg/util.go
/vendor/github.com/someuser/webserver/doc.go
/vendor/github.com/someuser/webserver/server.go
/vendor/github.com/someuser/webserver/vendor/github.com/someuser/utilpkg/util.go
```

This way, both versions of the `utilpkg` exists in the tree when Go needs to
compile them.

## Is this still relevant?

To a degree. It's not used anymore as gomodules fully supports dealing with
multiple different-versioned packages in a dependency chain.

But as gomodules still is somewhat of a new invention, it's still used by some
big packages out there in the OSS world.

## Can I mix vendoring and gomodules?

No. Not inside the same project. Either your project references packages as
modules, or references vendored projects.

Your dependency chain can however mix and match between vendoring and gomodules.

For example, you reference `utilpkg` and `webserver` via gomodules, and then
`webserver` still uses vendoring to reference `utilpkg`.

A single project can only either use vendoring or modules.

## References

- Mike Van Sickle. (2019, July 29). *Deep Dive into Go Packages* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-packages-deep-dive>
