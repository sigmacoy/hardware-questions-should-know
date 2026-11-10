# Memory Hierarchy and Caching

This document explains the hardware memory hierarchy and caching mechanisms. The explanations use ASD-STE100 principles.

## 1. What is the latency difference between an L1 cache hit and a main memory (RAM) access?

An L1 cache hit requires approximately one nanosecond or four processor cycles.
A main memory access requires 50 to 100 nanoseconds or hundreds of processor cycles.
When the processor waits for data from RAM, execution stalls.
Programmers must structure algorithms to keep frequently accessed data in the cache.
This practice avoids long processor stall cycles.

## 2. What is a cache line, and why does accessing array elements sequentially run faster than random pointer chasing?

A cache line is the minimum unit of data transfer between memory and cache, typically 64 bytes.
When a processor core reads one byte, the hardware loads the full 64-byte block.
Sequential array reads use every byte in that loaded cache line and trigger hardware prefetchers.
Following random pointers loads a new cache line for each access and discards the unused bytes.
Contiguous memory layouts therefore run much faster than linked data structures.

## 3. What is false sharing in multi-threaded programming, and how does it happen at the hardware cache level?

False sharing occurs when independent threads modify different variables that reside in the same cache line.
Hardware cache coherence protocols must invalidate the whole line across all cores during each write operation.
The cores continually invalidate each other's cache lines even when the program logic has no data conflicts.
This continuous cache invalidation degrades multi-threaded performance.
Software engineers must align or pad thread-local variables to separate cache lines.

## 4. What is a Translation Lookaside Buffer (TLB), and what causes a page fault?

A Translation Lookaside Buffer is a hardware cache that stores mappings from virtual addresses to physical memory addresses.
If an address is not in the TLB, the processor must walk page tables in main memory.
A page fault occurs when the requested page is not present in physical RAM or permissions are invalid.
The operating system must then load the page from secondary storage.
This storage access causes a large latency penalty.

## 5. What is the Memory Wall, and why are modern workloads more often memory-bandwidth bound than compute-bound?

The Memory Wall is the growing speed gap between processor computation and memory transfer rates.
Processors add arithmetic units rapidly, but memory buses do not supply data at that same rate.
Modern applications spend many clock cycles waiting for data delivery rather than computing results.
Software architects must design systems for data locality and memory bandwidth instead of raw operation counts.
