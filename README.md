# memoryallocator

A dynamic memory management library providing manual allocation, deallocation, and resizing of memory blocks.

## Project Overview

Memory management is a fundamental requirement in systems programming and performance-critical applications. The memoryallocator project implements a custom memory allocation system that gives developers fine-grained control over heap memory. Unlike standard library allocators, this project demonstrates a deep understanding of low-level memory operations, pointer arithmetic, and resource lifecycle management.

The allocator supports three core operations: allocating new memory blocks, freeing previously allocated blocks, and resizing existing blocks while preserving their contents. This makes it suitable for scenarios where memory usage patterns are known in advance or where deterministic allocation behavior is required.

## Core Features

- Dynamic memory allocation with configurable block sizes
- Safe deallocation of previously allocated memory regions
- In-place resizing of memory blocks with content preservation
- Memory block reuse to minimize fragmentation
- Boundary checking and null-pointer safety on all operations
- Clean separation between allocation logic and client code

## Technology Stack

- **C / C++**: The project is implemented in a systems-level language to provide direct memory access and minimal runtime overhead. This choice enables precise control over pointer operations and memory layout.
- **Standard Library (stdlib)**: Leverages standard memory primitives (malloc, free, realloc) as a baseline while extending functionality with custom allocation strategies.
- **Make / CMake**: Build system configuration for cross-platform compilation and easy integration into larger projects.

## Architecture and Design Decisions

The codebase follows a modular design with clear separation between the public interface and internal implementation details. The allocator exposes three primary functions: allocate, deallocate, and resize. Each function operates on opaque memory handles, hiding the internal bookkeeping structures from the caller.

Internally, the allocator maintains a free list of available memory blocks. When a new allocation is requested, the allocator searches the free list for a suitable block. If no block is large enough, it requests additional memory from the operating system. Deallocated blocks are returned to the free list and can be coalesced with adjacent free blocks to reduce fragmentation.

The design prioritizes simplicity and correctness over maximum performance. All operations include boundary checks and handle edge cases such as zero-size allocations and null pointers. The allocator does not use thread synchronization, making it suitable for single-threaded or externally synchronized environments.

## Installation and Setup

1. Clone the repository:
   ```
   git clone https://github.com/tvay11/memoryallocator.git
   cd memoryallocator
   ```

2. Build the project:
   ```
   make
   ```
   Or if using CMake:
   ```
   mkdir build && cd build
   cmake ..
   make
   ```

3. Run the test suite to verify the allocator works correctly:
   ```
   ./test_allocator
   ```

4. Include the allocator header in your own project:
   ```c
   #include "memoryallocator.h"
   ```

## Future Scope and Key Learnings

This project provided hands-on experience with low-level memory management, pointer manipulation, and the trade-offs involved in allocator design. Key learnings include the importance of alignment, the challenges of fragmentation, and the value of thorough testing for edge cases.

Future enhancements could include:
- Thread-safe allocation using mutexes or lock-free techniques
- Support for aligned allocations (e.g., for SIMD instructions)
- Memory pooling for fixed-size allocations
- Performance benchmarking against standard library allocators
- Integration with a garbage collection or reference counting system

The project serves as a foundation for understanding how memory allocators work under the hood and can be extended into a production-grade allocator for embedded or real-time systems.