---
date: 2021-01-24T12:31
tags:
  - go/best practices in golang
  - go/writing idiomatic golang code
  - go/create a lasting go project
---

# What to focus on in a Go project

Just getting the code to do what you want it is of course one of the key features
of your project. But ignoring the other aspects will lead your project to either
rot, discourage users from starting to use it or even stopping to use it, or
worst of all: make you, the maintainer, get tired of the project.

## Focus on the "customer"

Focusing on the features at hand may seem like the obvious choice, but it's
actually not the best choice. If you only att features with the mindset of
solving the problems, you risk your project getting bloated and eventually
difficult to add new features at all.

What to do focus on is trying to always trying to get into the perspective of the
consumer/customer/user of your project.

- Small and simple to use APIs.

  - [G20: Function Names Should Say What They Do](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/general/g20-function-names-should-say-what-they-do.html)
  - [N1: Choose Descriptive Names](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/names/n1-choose-descriptive-names.html)
  - [N3: Use Standard Nomenclature Where Possible](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/names/n3-use-standard-nomenclature-where-possible.html)

- Consistent naming and structure.


  - [G11: Inconsistency](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/general/g11-inconsistency.html)
  - [G24: Follow Standard Conventions](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/general/g24-follow-standard-conventions.html)

- Inviting to contributors by [[documenting-go-packages]] and keeping the code
  clean and clutter free.

  - [C2: Obsolete Comment](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/comments/c2-obsolete-comment.html)
  - [F4: Dead Function](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/functions/f4-dead-function.html)

- Easy to run the source code. If it's a convoluted procedure to set up your
  development environment, noone, not even you, will want to do it.

  - [E1: Build Requires More Than One Step](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/environment/e1-build-requires-more-than-one-step.html)
  - [E2: Tests Require More Than One Step](https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/environment/e2-tests-require-more-than-one-step.html)

## Do one thing, and do it well

The classical ["Unix philosophy"](https://en.wikipedia.org/wiki/Unix_philosophy)
that is echoed all over the place and phrased in different ways. The concept is
also commonly referred to as the *Single Responsibility Principle (SRP)*[^srp]
or the *Common Closure Principle (CCP)*[^ccp], and in turn relies on that you
design the system by [[volatility-decomposition]].

The idea is that your package should have a goal to solve, and it should not try
to touch anything outside its own scope. The term "bloat" often comes up when
a project fails to comply to this principle.

As your project grows, you probably want to extend its functionality anyway. This
should not be condemned, but you should then look into solving that with proper
integration or extensability instead.

## Integration support

A good package is a package that can integrate well with other existing
solutions.

Top example of this is password management. Instead of letting your project deal
with passwords, tokens, or other credentials itself, you should let the user be
able to integrate their existing password manage tools. For example, consider
the following config file:

```yaml
# ~/.config/mypkg.yaml

# BAD
apiKey: "7WGvzuQuONfPb7xT8GKgFb+edoD+nbyA"

# GOOD
apiKeyCommand: "pass show 'mypassword'"
```

This will mean you have to write more code, but results in giving the users more
options to choose from.

Other examples:

- Supporting multiple database providers, choosing between: "in memory", MySQL,
  MsSQL, PostgreSQL, etc.

- Supporting sending notifications via email, sms, as arguments to an arbitrary
  command, etc.

- Hosting the service inside Docker, Kubernetes, on "raw-metal", etc.

- Reading configuration through environment variables (`os.LookupEnv`), config
  files on disk, and command-line arguments.

## Extensability

Keeping a project extensible is a though task. This involves either supporting
some kind of plugin support or extensive configuration.

Prime examples are syntax highlighting libraries. It's very rare to find one that
only supports a handfull of languages, and that's it. Instead, they let you as a
user to create any new arbitrary syntax definitions that tells the parser how to
do its lexing/tokenization and parsing, so the syntax highlighter can even
support your [domain-specific language (DSL)](https://en.wikipedia.org/wiki/Domain-specific_language).

For Go library projects in particular, this means using interfaces properly so
your library consumers can switch out behaviors as they need.

## References

- Mike Van Sickle. (2019, July 29). *Deep Dive into Go Packages* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-packages-deep-dive>

- Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*
  (1st ed.). Pearson.

  - *Cited via* Metcalfe, D. (2019, January 22). *Clean Code: Smells and
    Heuristics.*
    <https://moderatemisbehaviour.github.io/clean-code-smells-and-heuristics/>

[^srp]: Martin, R. (2008). The Single Responsibility Principle. In *Clean Code: A Handbook of Agile Software Craftmanship* (*Robert C. Martin Series*) (1st ed., pp. 138-140). Pearson.
[^ccp]: Martin, R. (2017). The Common Closure Principle. In *Clean Architecture: A Craftsman’s Guide to Software Structure and Design* (*Robert C. Martin Series*) (1st ed., pp. 105–107). Pearson.
