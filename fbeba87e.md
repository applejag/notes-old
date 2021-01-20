---
date: 2021-01-20T18:32
tags: 
  - linux/how does memory work in linux
  - linux/what types of memory exists in linux
---

# Page mapping

The memory (RAM) in Linux is divided into
[page table entries](https://en.wikipedia.org/wiki/Page_table) to classify the
memorys use case. This is used by the Linux kernel to take informed decisions on
the memory based on its category/mapping type.

There are 5 distinct mapping types (categories) of memory.

## "Anonymous" memory

Commonly the heap and stack memory of an application. The source of the
information is from the application itself, in contrast to the other mapping
types that usually has a file as the source of truth.

## "Shared" memory

Almost as a superset of anonymous memory. An application can request a chunk of
shared memory that it can read and write to, just as with normal anonymous
memory.

What makes shared memory special is that it can, as the name suggests, be shared.
A process (application) can share a chunk of memory with a different process.
The data one process writes is readable by both processes, instantaniously.

Common use cases is to have processes communicate with each other in a highly
performant fashion. A form of RPC, if you will. Processes can talk to each other
in numerous ways, whereas using systems such as REST APIs, GRPC, or other
TCP/IP-based solutions may be more portable and easy to implement but are
magnitudes slower than using shared memory.

## "Cope on write" memory

Superset of shared memory, where the memory behaves as if it was only copied.

The process can initiate a chunk of memory to be copy-on-write memory, and all
processes that this memory is shared with can read from it. So far, identical
to shared memory.

Though when any of the processes writes to this chunk of memory it is first
duplicated (by the kernel) before recording the written data onto that new
clone. This makes the memory behave as if you only sent a chunk of memory to the
different processes, while saving some memory if it's only read by the other
processes.

## "File backed" memory

A cache of a files content.

Whenever you read from a file in Linux, the reading is done by the kernel that
buffers the content in memory before sending it off to the process/application
that requested it.

If the content of a file is requested while it is still buffered in memory, the
kernel will just use the already in-memory version of the file instead. This
gives a huge performance boost in a lot of use cases.

This buffering does take up as much memory as is available, but the file-backed
memory is considered low-priority so if a process tries to allocate more memory
than is currently free then the kernel will deallocate some file-backed memory
before letting the allocation from the process complete.

Deallocating file-backed memory is totally safe for the kernel to do at any time
as it builds on the assumption that the memory does have a source of truth:
the file on disk. File-backed memory is updated or removed for files that has
changed/been removed, so the content of a given file in memory is always
up-to-date or non-existent.

This process of allocating and deallocating file-backed memory is called
"swapping". Learn [[4b91deb2]].

## "Device backed" memory

In Linux, there's a fine line in the usage between a devices and a file.
Devices are considered files, but the information obtained from a device can not
live on the assumption that "if it's discarded then we can just obtain it again
by reading from the file again".

Example would be a keyboard. If a key is pressed, that is recorded by the kernel
and saved in device-backed memory to be read by a process. If the user types
<kbd>hello</kbd>, that data is stored in memory. But if that memory was
classified as low-prio, the same way as file-backed memory, then that memory
would potentionally be removed in favor of for example some anonymous memory.
If a process would then try to read data from this keyboard device, it may have
gotten replaced with the data from the user input <kbd>world</kbd>, resulting in
the <kbd>hello</kbd> input being forgotten completely.

## Swap memory

Swap memory is not strictly memory stored in your RAM. Swap more refers to how
your Linux kernel deals with running out of memory.

File-backed and anonymous memory are the only memory mappings that are affected
by swap. Read more about [[[4b91deb2]]] and how to control it via the
[[[1ae28f12]]] setting

## References

- McKay, D. (2019, December 9). *What Is Swappiness on Linux? (and How to Change
  It)*. How-To Geek. <https://www.howtogeek.com/449691/>
