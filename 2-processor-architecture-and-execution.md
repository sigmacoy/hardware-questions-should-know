# Processor Architecture and Execution

This document explains processor execution models and instruction scheduling. The explanations use ASD-STE100 principles.

## 1. What is the fundamental architectural difference between a CPU core and a GPU compute unit?

A CPU core contains large caches, deep branch predictors, and complex control logic to minimize latency for sequential tasks.
A GPU compute unit contains many simple execution units to maximize throughput for parallel data streams.
CPUs excel at complex branching and sequential execution.
GPUs excel at uniform arithmetic operations across thousands of independent data elements.

## 2. What is branch prediction, and why does an unpredictable if/else statement inside a tight loop degrade pipeline performance?

A branch predictor guesses the path of a conditional branch before the instruction evaluates.
This prediction lets the processor pipeline fetch and execute following instructions without waiting.
When the prediction is incorrect, the processor must flush the pipeline and discard all speculative work.
An unpredictable branch in a tight loop causes frequent pipeline flushes and reduces performance significantly.

## 3. What is SIMD (Single Instruction, Multiple Data) / vectorization, and how does a processor apply one instruction to 8 floats at once?

Single Instruction, Multiple Data uses wide hardware registers to process multiple values in parallel.
For example, a 256-bit vector register holds eight 32-bit floating-point numbers.
The hardware applies one arithmetic instruction across all eight numbers simultaneously in a single clock cycle.
Software developers must arrange data in contiguous arrays to permit vectorization by the compiler.

## 4. What is out-of-order execution, and why does hardware reorder instructions?

Out-of-order execution allows a processor to execute ready instructions instead of waiting for stalled instructions.
Hardware reorders instructions to keep execution units busy when an operation waits for memory.
The processor tracks dependencies and commits results in original program order to maintain correct behavior.
This mechanism hides memory latency but requires careful synchronization in concurrent software.

## 5. What is a memory barrier / fence, and why is it required for lock-free multi-threaded code?

A memory barrier is a hardware instruction that enforces ordering constraints on memory operations.
Compilers and out-of-order processors can reorder read and write operations for performance.
In multi-threaded code, another core can observe these memory operations out of sequence.
A memory fence prevents reordering across the boundary and makes memory operations visible in correct order.
