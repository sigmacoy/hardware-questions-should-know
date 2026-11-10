# Storage, I/O, and Networking

This document explains input/output operations, storage devices, and networking architecture. The explanations use ASD-STE100 principles.

## 1. How does reading sequentially from an NVMe SSD differ from random reads, and why do databases optimize for append-only logs (WAL / LSM-trees)?

NVMe solid-state drives read sequential blocks faster because the controller accesses internal flash channels in parallel.
Random write operations cause internal fragmentation, write amplification, and background block erase cycles.
Append-only logs write changes sequentially to the end of a file.
Databases use append-only logs and LSM-trees to maintain high write throughput and extend device operational life.

## 2. What is DMA (Direct Memory Access), and how does it let network cards and storage bypass the CPU?

Direct Memory Access lets hardware controllers transfer data directly to and from system RAM without CPU intervention.
The processor initializes the transfer parameters and then continues with other computational tasks.
The hardware controller signals an interrupt when the transfer is complete.
This mechanism frees processor cores from copying individual bytes between I/O devices and memory.

## 3. What is Zero-Copy networking, and why does moving data between kernel space and user space hurt high-frequency throughput?

Standard networking requires the operating system to copy data from kernel network buffers into application user space.
These repeated memory copies consume processor cycles, pollute CPU caches, and introduce latency.
Zero-Copy networking transfers data directly between device buffers and application memory using memory mapping or network interfaces.
High-throughput applications use Zero-Copy techniques to maximize network bandwidth and reduce processor workload.
