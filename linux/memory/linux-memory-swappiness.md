---
date: 2021-01-20T19:08
tags: 
  - linux/how does memory work in linux
  - linux/control the swap memory
  - linux/understanding swap and swappiness
  - linux/the vm.swappiness config
---

# Swappiness

Swappiness is a configuration value for the Linux kernel that controls how your
kernel will behave when it comes to swap memory. This setting is often referred
to as `vm.swappiness`. You can obtain your current swappiness value by reading
from the `/proc/sys/vm/swappiness` file:

```sh
$ cat /proc/sys/vm/swappiness
60
```

The setting falls in the range $swappiness \in \mathbb{Z} \cap [0, 100]$, i.e.
in the (inclusive) range of 0 to 100.

## How the setting affects swap

Your memory on your Linux machine is divided into different mappings. (Read more
about [[linux-memory-page-mapping]]). Your anonymous and file-backed memory both can
be cached to an effect on your disk and in your RAM, respectively.

Inside the Linux kernels source code, you will find the following:

```cpp
/*
* With swappiness at 100, anonymous and file have the same priority.
* This scanning priority is essentially the inverse of IO cost.
*/
anon_prio = swappiness;
file_prio = 200 - anon_prio;
```

Which means that

1. $anon\_prio \in \mathbb{Z} \cap [0, 100]$
2. $file\_prio \in \mathbb{Z} \cap [100, 200]$
3. As $anon\_prio$ increases, $file\_prio$ decreases.

Setting `vm.swappiness=0` does not disable swap, nor does setting
`swappiness=100` max out swap usage. What it does however, is control how the
prioritization of file-backed memory vs anonymous memory, and thereby how much
swap to focus on storing on the disk or storing in memory.

To be clear:

- **The lower the value, the more *willing* the kernel is to give up anonymous
  memory pages** and store it on disk in favor of file-backed memory.
  
- **The higher the value, the more *willing* the kernel is to give up file-backed
  memory** pages and need to retrieve files from disk more often in favor of not
  needing to store as much anonymous memory on disk.
  
- **You cannot tell the kernel to prefer file-backed pages over anonymous
  pages.** If you set `vm.swappiness=100`, then both `anon_prio=100` and
  `file_prio=100` so they receive equal amount of prioritization.

## Changing your computers swappiness

The `sysctl` is of great help here. You can change the current swappiness
directly without needing to reboot your computer by running:

```sh
$ sudo sysctl vm.swappiness=45
vm.swappiness = 45
```

The above will take action immediately.

The file `/etc/sysctl.conf` or file inside the `/etc/sysctl.d/` directory usually
has your computers swappiness written down. If you were to refresh these config
files or reboot your machine, the swappiness setting will be reset to factory
default or whatever is written in those files.

To make the swappiness change persitent, you need to save it in such a file. This
requires super-user (sudo) access. For example:

```sh
# Check if swappiness is already set in one of the mentioned files
$ grep --recursive swappiness /etc/sysctl.conf /etc/sysctl.d
# no output? => not specified in any .conf file.

# This assumes you don't have swappiness written down
$ echo "vm.swappiness=60" | sudo tee /etc/sysctl.d/20_swappiness.conf
```

## References

- McKay, D. (2019, December 9). *What Is Swappiness on Linux? (and How to Change
  It)*. How-To Geek. <https://www.howtogeek.com/449691/>
