---
date: 2021-01-20T21:23
tags: 
  - linux/how does memory work in linux
  - linux/what types of memory exists in linux
---

# Pages

Continuing on from [[linux-memory-zones]], the next segment abstraction of RAM in
Linux is pages. Each zone has a fixed set of pages, and each page has a fixed
set of bytes.

A process can request (allocate) any number of pages, but not any size other than
a multiple of the page size. Upon request of the memory page it obtains its
[[linux-memory-page-mapping]]# type, based on how it's requested.

The page size is determined on startup of your machine and cannot be changed
while memory is still in use. I.e. you need to reboot to change it. Most often
than not this value should not need to be tampered with though.

## Reading current page size

```sh
$ getconf PAGESIZE
4096
```

## References

- McKay, D. (2019, December 9). *What Is Swappiness on Linux? (and How to Change
  It)*. How-To Geek. <https://www.howtogeek.com/449691/>
