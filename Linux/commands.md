# Memory Concepts: Stack, Heap, and Memory Leaks

## Stack
- The stack is a special memory area used for managing function calls.
- It stores local variables, function parameters, and return addresses.
- Memory on the stack is automatically allocated and freed when functions are called and return.
- The stack size is usually small and limited.
- **Deep recursion** can cause a **stack overflow** because the stack runs out of space.

## Heap
- The heap is a larger, flexible memory area for dynamic memory allocation.
- Programs explicitly allocate (`malloc`, `calloc` in C; `new` in other languages) and free memory on the heap.
- The heap is managed manually by the programmer or automatically by the garbage collector in some languages.
- Heap memory persists until it is explicitly freed or garbage collected.
- Heap size is generally much larger than stack size.

## Memory Leak
- A memory leak occurs when a program allocates memory on the heap but never releases it.
- Even if the program no longer needs that memory, it remains allocated because references to it are lost or forgotten.
- Over time, memory leaks cause increased memory usage and can lead to the program or system running out of memory.
- Memory leaks usually happen due to improper management of heap memory, not stack memory.

## Key Differences: Stack vs Heap
| Feature             | Stack                             | Heap                              |
|---------------------|---------------------------------|----------------------------------|
| Memory management   | Automatic (function calls)       | Manual (allocation and deallocation) |
| Size                | Limited and smaller              | Larger and more flexible          |
| Lifetime            | Lasts until function returns     | Lasts until explicitly freed     |
| Usage               | Local variables, call frames     | Dynamic objects, data structures  |
| Speed               | Fast allocation and deallocation | Slower due to complex management  |

---

# Summary

- The **stack** manages function calls and local variables with automatic memory handling.
- The **heap** handles dynamic memory allocation which needs manual or garbage collected management.
- **Memory leaks** happen when heap memory is not properly freed.
- Programs use both stack and heap memory for different purposes.

