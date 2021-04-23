---
date: 2021-04-22T20:04
---

# Binary search tree - Removing a node

The actions you need to take when removing a node depends on the state of the
soon-to-be-removed node.

```fsharp
let removeNode node root =
    match node with
    | { Left = None; Right = None } -> removeLeaf node root
    | { Left = None } | { Right = None } -> removeParentOf1 node root
    | _ -> removeParentOf2 node root
```

## Leaf node

Just remove it. The tree will not be affected. This is why the "post-ordering"
enumeration is so great, as explained in [[binary-search-tree-enumeration]].

```fsharp
let removeLeaf node root =
    // recursive descent
    // rebuild all parent nodes of target node all the way up to root
    // in a balanced tree, and on average, this would take O(log n) operations
```

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

```fsharp
let removeParentOf1 node root =
    // recursive descent down to parent of node
    // rebuild all nodes but with child taken place of target node
    // all the way up to the root node
    // in a balanced tree, and on average, this would take O(log n) operations
```

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

- If the right node (`F`) does not have a left node, then promote that node
  (`F`) instead.

- The right node's right nodes (`G`) are completely ignored.

- The promoted child is guaranteed to not have a left node, as we take the
  leftmost node.

- The promoted child has itself removed from the old parent's right branch.

```fsharp
let leftmost node =
    match node.Left with
    | Some child -> leftmost child
    | None -> node

let removeParentOf2 node root =
    let childToPromote = oldNode |> Option.map leftmost
    let newRightBranch = root.Right |> Option.map (removeLeaf childToPromote)

    { childToPromote with
      Left = oldRoot.Left
      Right = newRightBranch  }
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
