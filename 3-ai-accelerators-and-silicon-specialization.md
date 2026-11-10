# AI Accelerators and Silicon Specialization

This document explains specialized hardware architectures for artificial intelligence and matrix processing. The explanations use ASD-STE100 principles.

## 1. What is an AI chip (NPU/TPU), and why does it use a systolic array instead of standard register files for matrix multiplication?

An AI accelerator is specialized silicon designed for tensor operations and matrix multiplication.
A systolic array connects arithmetic units in a physical two-dimensional grid.
Data flows directly from one arithmetic unit to the next unit without reading or writing registers each time.
This direct data transfer eliminates register read cycles and greatly reduces energy consumption.

## 2. Why do neural networks train and infer on reduced precision (BF16, FP8, INT8) instead of standard FP32 or FP64?

Neural network calculations tolerate small numerical errors without significant loss in final accuracy.
Lower precision formats consume half or one quarter the memory footprint of 32-bit floating-point values.
Smaller data sizes reduce memory bandwidth demands and let hardware execute more arithmetic operations per cycle.
Software systems use quantization to fit larger models into available memory and increase execution speed.

## 3. What is High Bandwidth Memory (HBM), and why is it used on modern server accelerators instead of standard DDR5?

High Bandwidth Memory stacks memory dies vertically on a silicon interposer near the processor.
This physical design provides a very wide memory bus with thousands of data traces.
Standard DDR5 memory connects across a circuit board and provides narrower bus widths.
AI accelerators use High Bandwidth Memory because large tensor operations require terabytes per second of memory bandwidth.

## 4. What is the difference between latency-oriented hardware (CPUs) and throughput-oriented hardware (GPUs)?

Latency-oriented hardware minimizes the elapsed time required to complete an individual task.
CPUs use large caches and high clock frequencies to execute single threads quickly.
Throughput-oriented hardware maximizes the total amount of work completed in a unit of time.
GPUs use thousands of smaller cores to hide memory latency by executing many parallel threads.
