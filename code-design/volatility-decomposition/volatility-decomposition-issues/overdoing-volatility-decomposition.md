---
date: 2021-02-15T19:35
tags: 
  - code design/issues with volatility decomposition
---

# Overdoing volatility decomposition

When you're designing a system using #[[volatility-decomposition]], a common trap to
fall into is to encapsulate everything. This is especially prominent when you are
[[finding-the-nature-of-your-buisness]]# or [[finding-a-systems-components]].

Most important thing to remember: Not everything needs its own block/component.

Designing so every subset of your system needs its own block is called
designing using [[functional-decomposition]].

## Song of the siren

Volatility-based decomposition is hard work, and function-based decomposition is
easy, ergo it's utterly easy to procastinate your design process by doing
functional decomposition. In this case, [[functional-decomposition]]# is the
[[song-of-the-siren]]#.

> "Tie yourself to the mast and sing, loudly,
>
>     'IF IT IS NOT VOLATILE, THEN THERE IS NO BLOCK'
>     'IF IT IS NOT VOLATILE, THEN THERE IS NO BLOCK'
>     'IF IT IS NOT VOLATILE, THEN THERE IS NO BLOCK'
> 
> until you've convinced yourself"
> --- J. Löwy (January 27, 2021)

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
