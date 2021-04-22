---
date: 2021-04-22T20:04
---

# Binary search tree - Removing a node

The actions you need to take when removing a node depends on the state of the
soon-to-be-removed node.

## Leaf node

Just remove it. The tree will not be affected. This is why the "post-ordering"
enumeration is so great, as explained in [[binary-search-tree-enumeration]].

```{.mermaid}
graph TD
    subgraph after C removed
    D2[D]==>B2[B]
    D2[D]==>F2[F]
    F2[F]==>E2[E]
    F2[F]==>G2[G]
    end

    subgraph before C removed
    D1[D]==>B1[B]
    D1[D]==>F1[F]
    B1[B]==>C1((C))
    F1[F]==>E1[E]
    F1[F]==>G1[G]
    end
```

## Parent of 1

You promote the single child to where the removed parent once was.

```{.mermaid}
graph TD
    subgraph after B removed
    D2[D]==>C2[C]
    D2[D]==>F2[F]
    F2[F]==>E2[E]
    F2[F]==>G2[G]
    end

    subgraph before B removed
    D1[D]==>B1((B))
    D1[D]==>F1[F]
    B1((B))==>C1[C]
    F1[F]==>E1[E]
    F1[F]==>G1[G]
    
    C1-.->B1
    end
```

## Parent of 2

Here it gets a little more complicated as we need to conform to the rules
defined for a [[binary-search-tree]].

The algorithm goes: Promote the *leftmost node* of the *right node*.

```fsharp
let leftmost node =
    match node.Left with
    | Some child -> leftmost child
    | None -> node
    
let childToPromote node =
    match node.Right with
    | Some child -> Some (leftmost child)
    | None -> None
    
let root = ...
let newRoot = { root with Left = root.Left; Right = childToPromote root }
```

```{.mermaid}
graph TD
    subgraph after D removed
    E2[E]==>B2[B]
    E2[E]==>F2[F]
    B2[B]==>C2[C]
    F2[F]==>G2[G]
    end

    subgraph before D removed
    D1((D))==>B1[B]
    D1((D))==>F1[F]
    B1[B]==>C1[C]
    F1[F]==>E1[E]
    F1[F]==>G1[G]
    
    E1-.->D1
    end
```

## Reference

- Robert Horvick (2020, June 16). *Algorithms and Data Structures - Part 1*
  [Course]. Pluralsight. <https://www.pluralsight.com/courses/algorithms-data-structures-part-one>
