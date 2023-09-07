# Malloc Implementation in C

This project provides a custom implementation of memory management functions: `malloc()`, `free()`, `calloc()`, and `realloc()` in C.

## Features

- Double Linked List based memory management.
- Uses `sbrk` for memory allocation.
- Implementations for `malloc`, `free`, `calloc`, and `realloc`.
- Automatic memory splitting and coalescing for optimizing memory usage.

## Structure

The primary data structure used is a double linked list node:

```c
struct node {
    int size;
    int free;
    struct node* prev;
    struct node* next;
    void* start;
};
```

Each node represents a block of allocated or free memory.

## Functions

- `void* malloc(size_t size)`: Allocates `size` bytes of memory.
- `void free(void* ptr)`: Frees the memory pointed to by `ptr`.
- `void* calloc(size_t num_of_elts, size_t elt_size)`: Allocates and initializes to zero the memory for an array.
- `void* realloc(void* pointer, size_t size)`: Re-allocates `pointer` to new size `size`.

## Dependencies

- `<stdio.h>`
- `<sys/types.h>`
- `<unistd.h>`
- `<errno.h>`
- `<math.h>`

## Usage

To compile and run the program, execute:

```bash
gcc malloc.c -o malloc
./malloc
```
