# Instruction Set Architectures and the Compiler Boundary

This document explains instruction set architectures, binary interfaces, and compiler execution boundaries. The explanations use ASD-STE100 principles.

## 1. What are the key architectural differences between x86-64, ARM, and RISC-V instruction sets?

CISC architectures like x86-64 provide variable-length instructions that perform complex operations in single instructions.
RISC architectures like ARM and RISC-V use fixed-length instructions with simpler operations and more general-purpose registers.
Variable-length instructions require complex decoder hardware that consumes significant silicon area and electrical power.
Compilers for RISC architectures generate more instructions, but the processor decodes them with higher efficiency.

## 2. What is endianness, and how does byte ordering affect network serialization and binary parsing?

Endianness defines the order in which a computer stores multi-byte values in memory.
Little-endian systems store the least significant byte at the lowest memory address.
Big-endian systems store the most significant byte at the lowest memory address.
Network protocols use big-endian order, whereas most modern consumer processors use little-endian order.
Software engineers must convert byte ordering explicitly during binary serialization to avoid data corruption.

## 3. What is an Application Binary Interface (ABI), and how do calling conventions pass function arguments?

An Application Binary Interface defines the low-level contract for how software components interact at machine level.
Calling conventions specify which processor registers hold function arguments and return values.
Modern calling conventions pass initial function arguments in registers and use the stack only for overflow arguments.
Register-passing executes function calls quickly, whereas stack-passing requires memory store and load instructions.

## 4. What is instruction pipelining, and what causes pipeline stalls or bubbles?

Instruction pipelining divides execution into discrete sequential stages: Fetch, Decode, Execute, and Writeback.
Multiple instructions advance through these stages concurrently across consecutive clock cycles.
A pipeline stall occurs when an instruction must wait for a memory read, branch decision, or execution unit.
Stalls insert idle cycles called bubbles into the pipeline, which reduces processor instruction throughput.
