# Power, Thermals, and Embedded Constraints

This document explains energy constraints, thermal throttling, and heterogeneous hardware architectures. The explanations use ASD-STE100 principles.

## 1. What is Thermal Design Power (TDP), and how does thermal throttling affect software execution?

Thermal Design Power is the maximum amount of heat that a cooling subsystem can dissipate under normal operation.
Dynamic Voltage and Frequency Scaling reduces clock frequency when silicon temperatures exceed safe operating limits.
A "race-to-sleep" strategy runs tasks at maximum speed so the processor can return to low-power idle quickly.
Sustained workloads must remain within thermal limits to prevent unexpected hardware throttling and latency spikes.

## 2. What is heterogeneous computing, and how do operating systems schedule threads across performance and efficiency cores?

Heterogeneous architectures place high-performance cores and energy-efficient cores on the same silicon die.
Performance cores provide high clock frequencies and wide pipelines for latency-critical application threads.
Efficiency cores run at lower voltages to process background tasks with minimal electrical energy.
Operating systems use thread affinity and load schedulers to assign each thread to the optimal core type.

## 3. What is Unified Memory Architecture (UMA), and how does it eliminate PCIe transfer overhead?

Unified Memory Architecture provides a single physical memory pool shared by the CPU, GPU, and neural accelerator.
All processor units access this memory with high bandwidth and direct hardware coherency.
Traditional discrete architectures must copy data over the PCIe bus between main memory and graphics memory.
Unified memory removes these PCIe copy operations and lets software share data pointers directly across compute devices.

## 4. How do polling and wake locks cause battery drain in power-constrained devices?

Mobile and embedded processors consume significant electrical power each time they exit low-power sleep states.
Memory polling loops prevent the CPU from entering low-power idle and drain battery reserves continuously.
Software must use hardware interrupts and event notifications instead of active polling.
Applications must release wake locks promptly and batch network operations to maximize idle sleep duration.
