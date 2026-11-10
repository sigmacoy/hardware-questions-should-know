# Hardware Questions Every Software Engineer Should Know

> Production-first questions, mental models, and architectural patterns for Systems and Software Engineers. Written in Simplified Technical English (ASD-STE100 rules).

---

## Overview

Understanding hardware does not require designing physical silicon chips. In the software industry, this understanding is called **mechanical sympathy**. A racing driver does not build the engine from raw steel. The driver knows how the transmission, torque, and tires operate to drive faster without vehicle failure.

Software engineering shares this principle. Knowing where data lives and how processors execute instructions lets you build reliable, high-performance systems.

This repository is a structured engineering guide focused on silicon mechanics, architectural trade-offs, and hardware-level performance boundaries.

---

## The Core Mental Model

You do not need circuit diagrams or Verilog code. You only need to answer three physical questions:

1. **Where does the data live?**
   Registers $\rightarrow$ L1/L2/L3 Cache $\rightarrow$ RAM $\rightarrow$ NVMe SSD / Network. Each step outward increases access latency by an order of magnitude.

2. **Is the workload compute-bound or memory-bound?**
   Is execution limited by arithmetic units or by memory bus transfer speed? Most modern production software is memory-bandwidth bound.

3. **Is the execution sequential or parallel?**
   Complex branching belongs on latency-optimized CPU cores. Large-scale matrix arithmetic belongs on throughput-optimized GPU or NPU accelerators.

---

## Table of Contents

- [01. Memory Hierarchy & Caching](1-memory-hierarchy-and-caching.md) — Cache hit latencies, 64-byte cache lines, false sharing, TLB, page faults, and the Memory Wall.
- [02. Processor Architecture & Execution](2-processor-architecture-and-execution.md) — CPU vs. GPU compute units, branch prediction, SIMD vectorization, out-of-order execution, and memory barriers.
- [03. AI Accelerators & Silicon Specialization](3-ai-accelerators-and-silicon-specialization.md) — Systolic arrays, reduced precision (BF16/FP8/INT8), High Bandwidth Memory (HBM), and throughput architecture.
- [04. Storage, I/O & Networking](4-storage-io-and-networking.md) — NVMe sequential vs. random reads, append-only logs (WAL/LSM-trees), Direct Memory Access (DMA), and Zero-Copy networking.
- [05. ISA & The Compiler Boundary](5-isa-and-compiler-boundary.md) — x86-64 vs. ARM vs. RISC-V, endianness, ABI calling conventions, and instruction pipelining stalls.
- [06. Hardware Security & Isolation](6-hardware-security-and-isolation.md) — Privilege rings (Ring 0 vs. Ring 3), VT-x/AMD-V virtualization, speculative execution side channels, and Secure Enclaves.
- [07. Power, Thermals & Embedded Constraints](7-power-thermals-and-embedded-constraints.md) — TDP, DVFS thermal throttling, heterogeneous cores (big.LITTLE), Unified Memory Architecture (UMA), and battery optimization.

---

## Related Repositories

- [cs-questions-should-know](https://github.com/sigmacoy/cs-questions-should-know) — Core data structures, algorithms, operating systems, and networking.
- [applied-ai-questions-should-know](https://github.com/sigmacoy/applied-ai-questions-should-know) — Production AI, embeddings, RAG, and inference systems.
- [fintech-questions-should-know](https://github.com/sigmacoy/fintech-questions-should-know) — Distributed transactions, ledgers, payment rails, and auditability.
