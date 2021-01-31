---
date: 2021-01-31T11:35
tags: 
  - programming/how not to design software
  - programming/why functional decomposition is bad
---

# Locking in to vendors

> A vendor in this context refers to a library author. Could be a company with
> propriatary code, or just some hobbyist that has an open source repo.
>
> Examples would be database APIs or ORMs, UI framworks, runtimes, et.c.

What does the documentation of a vendor tell you? It tells you how to lock
yourself into their library. This is not a devious intention from the authors,
but they still want you to stick to using their tool as long as possible.

Therefore they're not careful about telling you to sprinkle dependencies upon
their tool all over your code base. When you want to change it, you'll notice
that you're so committed to this existing tool, and it would be such a task to
remove the dependency, that you instead put effort on making it work *anyway*.

## Switching out a vendor

The work that has to be put in to switch a library vendor usually means having
to visit all your services, given you've followed #[[functional-decomposition]]
during the design process.

Isolating the use of the vendor would resolve this, but this is very difficult
as long as you still follow #[[functional-decomposition]].

## Read between the lines

How to properly interpret implementation documentation is **how not to do it!**

If you **do not** follow their guides, and instead focus on keeping them at arms
length during the implementation and focusing on being able to switch them out
at any given time, then doing so will be possible.

This means more work up front, but less work down the path. The wording of
"locking yourself in to a vendor" is not an exaggeration, it's a realistic
warning.

## Examples

Programming examples:

- **Entity Framework:** A .NET ORM that for one allows you to segregate the
  vendor lock-in from the different databases, but you still heavily rely on EF.
  Switching to a different ORM, such as Dapper or NHibernate would lead to huge
  amount of work in most cases.
  
- **.NET**: The platform has been praised lately for its portability. But if you
  write something in C\# for example today, can you simply port that code over to
  a different platform, say Java, or Go?

  There are few languages that actually has good interopability. C is one of them
  with their libraries that most language support interop with. How much do you
  want to lock in to using .NET?

Non-programming related examples:

- **Drugs:** Go to a pharmacy and say you have a headache. They will promptly
  redirect you to their collection of medicines you can consume that will resolve
  your problems. The vendors in this case is the companies producing the drugs.

  Now instead go to a doctor with the same symptom and ask for advice. The
  doctor, given they are an uncorrupted doctor, will just suggest some exercise
  or consuming some more vegetables and water.

- **Car:** Is it easy to buy a car today? If you go to a retailer, you will have
  no idea if you've gotten the best car for your buck that suits your needs. The
  vendors in the case is the companies behind the cars.
  
  Exchaning a car part today does not mean ordering "kind of the same part",
  you must order the exact part made for that exact car for that exact brand,
  from that exact vendor.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.

