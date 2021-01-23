---
date: 2021-01-20T21:30
tags: 
  - linux/how does memory work in linux
  - linux/what types of memory exists in linux
---

# Linux memory layout

Your RAM in Linux is built upon the following abstractions:

- Each CPU (multi-core or not) is associated to their own [[[linux-memory-nodes]]], ex: Node 0.

  - Each node is made up of [[[linux-memory-zones]]], ex: DMA, DMA32, Normal.

    - Each zone contains a set number of [[[linux-memory-pages]]], usually at the size of 4096
      bytes.

      - Each page can have a [[[linux-memory-page-mapping]]], ex: anonymous, file-backed,
        device-backed.
    
The Linux kernel can alter how file-backed and anonymous mapped pages are stored
by moving them back and forth between RAM and disk. This is referred to as
"swapping". Read [[[how-linux-uses-swap]]]

## References

- McKay, D. (2019, December 9). *What Is Swappiness on Linux? (and How to Change
  It)*. How-To Geek. <https://www.howtogeek.com/449691/>
