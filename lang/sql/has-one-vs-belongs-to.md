---
date: 2021-11-04T09:51
tags:
  - sql/relations
  - go/gorm
---

# Has-One vs Belongs-To

Both regards 1:1 (one to one) relations, but implies different behaviour

## Sample models

A user can have 1 calender, and 1 calender can only be used by 1 user. Using [[go]]
 as sample language, and behaviour may be specific to GORM.

```go
type User struct {
    ID        uint
    FirstName string
    LastName  string
}

type Calender struct {
    ID   uint
    Name string
}
```

## Has-One

The subject model is the owner.

If `User` has one `Calender`, then the `User` is the owner of the `Calender`.

```go
type User struct {
    ID        uint
    FirstName string
    LastName  string
    Calender  Calender // <--
}

type Calender struct {
    ID     uint
    Name   string
    UserID uint // <--
}
```

Implies:

- if `User` is deleted, then so is `Calender`.
- if `Calender` is deleted, then `User` *could* stick around.

## Belongs-To

The subject model is the target.

If `User` belongs to `Calender`, then the `Calender` is the owner of the `User`.

```go
type User struct {
    ID          uint
    FirstName   string
    LastName    string
    Calender    Calender // <--
    CalenderID  uint     // <--
}

type Calender struct {
    ID     uint
    Name   string
}
```

Implies:

- if `Calender` is deleted, then so is `User`.
- if `User` is deleted, then `Calender` *could* stick around.

## References

- Mike Van Sickle. (2016, February 2). *GORM: An Object Relational Mapper for Go* [Course].
  Pluralsight. <https://pluralsight.com/courses/gorm-go-object-relational-mapper>
