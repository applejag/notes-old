---
date: 2021-04-22T20:04
---

# Binary search tree

Commonly shortened as: BST

Data structure is made up of nodes. Usually looks something like this:

```fsharp
type bstNode<'T> =
  { Value: 'T
    Left: bstNode<'T> option
    Right: bstNode<'T> option }
```

## Rules

- Every node in the `.Left` branch has a lower (or equal) value than `.Value`
- Every node in the `.Right` branch has a higher value than `.Value`
- Every node is immutable

## Benefits

Main benefit is the speed of operations.

| Operation | Average    | Worst |
| --------- | ---------- | ----- |
| Add       | $O(\log n)$ | $O(n)$ |
| Remove    | $O(\log n)$ | $O(n)$ |
| Find      | $O(\log n)$ | $O(n)$ |

## Terminology

- A container of a single value and pointers to the next containers is called a
  *"node"*.
  
- The nodes referenced by a node are called *"child nodes"* and
  *"parent nodes"*

- The `D` node lacks parent, and is therefore called the *"root node"*.

- The `A`, `C`, `E`, `G` nodes lacks children, and is therefore are called the
  *"leaf nodes"*.

```{.mermaid}
graph TD
    D==>B
    D==>F
    B==>A
    B==>C
    F==>E
    F==>G
```
