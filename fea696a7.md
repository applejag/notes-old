---
date: 2021-01-20T21:37
tags: 
  - linux/how does memory work in linux
  - linux/what types of memory exists in linux
---

# Nodes

One CPU chip, wether it is multi-core or not, has node associated with it.

Nodes in Linux has a very straight forward naming format for their nodes.
Starting at "Node 0", incrementing for every node (Node 0, Node 1, Node 2, ...).

Your computer probably only has 1 node: Node 0. You can see the list of nodes
and their associated [[[linux-memory-zones]]] by running:

```sh
$ less /proc/buddyinfo
Node 0, zone      DMA      1      0      0      1      2      1      1      0      0      1      3 
Node 0, zone    DMA32      3      2      4      3      6      4      4      4      3      1    963 
Node 0, zone   Normal    287    247    152     88     56     21     18      4      5     13   1687 
```

Ignore the number columns. The meaning of them are for memory diagnostics, and
will not be going that through here.

## References

- McKay, D. (2019, December 9). *What Is Swappiness on Linux? (and How to Change
  It)*. How-To Geek. <https://www.howtogeek.com/449691/>
