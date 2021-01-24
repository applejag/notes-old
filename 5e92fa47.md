---
date: 2021-01-24T13:28
tags: 
  - go/best practices in golang
  - go/writing idiomatic golang code
  - go/create a lasting go project
---

# When to use structs or interfaces

The Go language has two main data types that you fondle around with: interfaces
and structs.

```go
type MyStruct struct {
    Field1 string
    Field2 int
}

type MyInterface interface {
    Func1(string)
    Func2() string
}
```

## When to use structs

A `struct` type can hold fields, but cannot be extended with more information.
It's a static data-container.

This means that you should be careful when using structs as a library consumer
of your project may want to add data to their data containers here and there
depending on their use case.

## Structs: Configs

A common "good practice" use case for structs are configs. For example, here's a
config for some generic web hosting service:

```go
package server

type Config struct {
    Port     int
    Hostname string
}
```

Good example of this is the `http.Request`, which is a configuration of how a
HTTP request should be sent.

This can however go bad when you want to let the library consumer to define what
database to use. MsSQL uses connection strings, Postgres uses username+password;
how do you support both scenarios without bloating up your config with a lot of
fields that will be unused in either case?

This is where you'd mix the config with some interfaces and let the consumers
initialize and define their own configs for their database implementation. Not
all configs should be declared by you, but generally speaking: all configs should
be structs.

## Structs: Return types

If you library accepts a structs as an argument, then the library consumer must
use your data types and cannot extend the configurations of their custom
behavior in any clean way.

But return types are a different story. The data returned from a method should
not need to be altered. Good example of this is the `http.Response` type. A HTTP
response does always have a status code, a body, list of headers, et.al. A
library consumer should not need to extend the data in this response, or
otherwise they're using the wrong library to begin with.

## Interfaces: Behavior

Any time you need to declare some behavior, you should do that via an interface.
Doing that will make the project both more testable and more extensible.

Consider the web server with database example mentioned above. If we want to
access the database, we could either *lazily* just hardcode a MySQL dependency
into the functions:

```go
type Config struct {
    DatabaseURL   string
    MySQLUsername string
    MySQLPassword string
}

func FetchUserById(config Config, id int) (User, error) {
    // This is pseudo-code. Not tested nor using real APIs
    conn := db.Connection(config.DatabaseURL, config.MySQLUsername, config.MySQLPassword)
    user := conn.Select("Users").Where("UserId = ?", id).Single()
    return user, nil
}
```

The above locks the library user to

1. Use MySQL
2. Provide MySQL credentials through the library's `Config` struct

A cleaner and more extensible solution would be:

```go
type Config struct {
    DB *Database
}

type Database interface {
    FetchUserById(int) (User, error)
}

type MySQLDatabase struct {
    Url      string
    Username string
    Password string
}

func (db *MySQLDatabase) FetchUserById(id int) (User, error) {
    // This is pseudo-code. Not tested nor using real APIs
    conn := db.Connection(db.Url, db.Username, db.Password)
    user := conn.Select("Users").Where("UserId = ?", id).Single()
    return user, nil
}

func FetchUserById(config Config, id int) (User, error) {
    return config.DB.FetchUserById(id)
}
```

The type `MySQLDatabase` is in this case an implementation provided by the
library, but the library consumer can very well just *not* use that
implementation and instead add their own `Database` implementation that may very
well just use Postgres, some in-memory store, or just direct file access.

This is also talked about in [[[what-to-focus-on-in-a-go-project]]] in its section
about integration and extensibility. It's more work, but it's worth it.

## Interfaces: errors

Errors is a classic example of interfaces. The `error` type is **always** what
you want to use when returning errors.

The `error` interface looks like this:

```go
type error interface {
    Error() string
}
```

This means that the error you produce in your code can conform to this interface
and then store any information you'd want in it.

The most basic implementation of this is the error you'd find in the `errors`
standard package:

```go
package errors

// New returns an error that formats as the given text.
// Each call to New returns a distinct error value even if the text is identical.
func New(text string) error {
	return &errorString{text}
}

// errorString is a trivial implementation of error.
type errorString struct {
	s string
}

func (e *errorString) Error() string {
	return e.s
}
```

It just stores a string. And that's it.

This is very benifitial in some cases such as if you run a process and have it
error on non-zero exit code, then the error could have an integer field with the
exit code that the consumer could take use of instead of trying to parse that
value out from the error message string, which would be very volatile of a
solution.

## References

- Mike Van Sickle. (2019, July 29). *Deep Dive into Go Packages* [Course].
  Pluralsight. <https://www.pluralsight.com/courses/go-packages-deep-dive>
