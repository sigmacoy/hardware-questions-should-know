# Hardware Security and Isolation

This document explains hardware isolation boundaries, virtualization, and processor security features. The explanations use ASD-STE100 principles.

## 1. What are hardware privilege rings, and why do system calls create performance overhead?

Hardware privilege rings enforce execution boundaries between user software in Ring 3 and operating system routines in Ring 0.
Ring 0 instructions can manage hardware interrupts, manipulate page tables, and access control registers directly.
A system call forces the processor to change privilege levels, save register state, and switch page tables.
High-performance software minimizes system calls to eliminate repeated privilege boundary transitions.

## 2. What are hardware virtualization extensions, and how do they enable virtual machines to run at near-native speed?

Hardware virtualization extensions provide a dedicated CPU mode for hypervisors below standard operating system rings.
Processors with these extensions use nested page tables to translate guest physical addresses directly to host physical addresses.
This hardware support allows virtual machines to execute guest instructions directly on the physical CPU without software emulation.
As a result, virtualized operating systems achieve near-native execution performance with strong hardware isolation.

## 3. What are speculative execution side-channel vulnerabilities, and how do they leak data across memory boundaries?

Speculative execution predicts branch targets and executes following instructions ahead of time.
When a branch prediction is incorrect, the processor discards the architectural state but leaves traces in cache lines.
Attacks such as Spectre read these cache timing differences to extract secret data across process boundaries.
Software must use speculation barrier instructions and compiler mitigations to protect sensitive data from side-channel exposure.

## 4. What are Secure Enclaves and Trusted Platform Modules (TPM), and how do they protect cryptographic keys?

A Trusted Platform Module provides hardware-level cryptographic key generation, secure storage, and platform integrity measurement.
A Secure Enclave creates an isolated execution environment in memory that the hardware encrypts independently.
Administrative users and compromised operating system kernels cannot read or alter enclave memory contents.
Software systems use enclaves and TPMs for confidential cloud computing and remote attestation.
