---
date: 2021-05-05T19:27
tags:
  - pluralsight
---

# Set

A set is a collection in which:

- Each item is distinct. There are no duplicates
- There's no sense of order. You cannot sort a set.

| Operation            | Syntax          | Example                                         |
| ---------            | ------          | -----------                                     |
| Union                | $A \cup B$      | $\{1, 2, 3\} \cup \{2, 3, 4\} = \{1, 2, 3, 4\}$ |
| Intersection         | $A \cap B$      | $\{1, 2, 3\} \cap \{2, 3, 4\} = \{2, 3\}$       |
| Set difference       | $A - B$         | $\{1, 2, 3\} - \{2, 3, 4\} = \{1, 2\}$          |
| Symmetric difference | $A \triangle B$ | $\{1, 2, 3\} \triangle \{2, 3, 4\} = \{1, 4\}$  |

## Union $A \cup B$

1. Copy set $A$ into set $X$
2. Add all values of set $B$ into set $X$, skipping duplicates

## Intersection $A \cap B$

1. New empty set $X$

2. Foreach value in $A$

   - If it's not in $B$, then add to $X$

2. Foreach value in $B$

   - If it's not in $A$, then add to $X$

## Set difference $A - B$

1. Copy set $A$ into set $X$
2. Remove all values of set $B$ from set $X$, skipping values that don't exist.

## Symmetric difference $A \triangle B$

Can be calculated using the previous operations:

$$
A \triangle B = (A \cup B) - (A \cap B)
$$

For example:

$$
\begin{align}
\{1,2,3\} \triangle \{2,3,4\} &= (\{1,2,3\} \cup \{2,3,4\}) - (\{1,2,3\} \cap \{2,3,4\}) \\
&= \{1,2,3,4\} - \{2,3\} \\
&= \{1,4\}
\end{align}
$$

## Naming differences in .NET

| Math                 | .NET `HashSet<T>`                                   |
| ----                 | ----                                                |
| Union                | [`.UnionWith(IEnumerable<T>)`][dotnetUnion]                       |
| Intersection         | [`.IntersectWith(IEnumerable<T>)`][dotnetIntersect] |
| Set difference       | [`.Except(IEnumerable<T>)`][dotnetExcept]                         |
| Symmetric difference | [`.SymmetricExceptWith(IEnumerable<T>)`][dotnetSymmetricExcept]   |

## Reference

- Robert Horvick (2020, November 2). *Algorithms and Data Structures - Part 2*
  [Course]. Pluralsight. <https://www.pluralsight.com/courses/algorithms-data-structures-part-two>

[dotnetUnion]: https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1.unionwith
[dotnetIntersect]: https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1.intersectwith
[dotnetExcept]: https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1.exceptwith
[dotnetSymmetricExcept]: https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1.symmetricexceptwith
