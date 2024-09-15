# Heap Memory Manager

## Overview

This project simulates a simple heap memory manager in C, which allows users to allocate, free, and manage blocks of memory in a custom heap. The program mimics the behavior of dynamic memory allocation (`malloc`/`free`) by manually managing memory blocks on a statically allocated heap of size 1024 bytes.

## Features

1. **Custom Memory Allocation**:
   - Allocate memory for `int`, `double`, and `string` values.
   - The memory allocation is done by searching the heap for free blocks that can satisfy the request.

2. **Memory Freeing**:
   - Free allocated memory by specifying the pointer and merge adjacent free blocks to prevent fragmentation.

3. **Heap Initialization and Re-initialization**:
   - The heap is initialized with a single free block of size 1024 bytes.
   - The user can deallocate the entire heap and re-initialize it.

4. **Memory Block Merging**:
   - Merge adjacent free blocks to reduce fragmentation in the heap.

5. **Display Heap Status**:
   - Print the current status of the heap, showing block sizes, whether they are allocated or free, and display data for allocated blocks.

## Code Structure

### Main Components:

1. **Block Structure**:
   - Represents a block of memory in the heap.
   - Contains fields for block size, allocation status (free or allocated), and a pointer to the next block.

2. **Heap Initialization**:
   - The heap is initialized as a linked list of blocks, starting with a single free block of 1024 bytes minus the overhead for the block metadata.

3. **Memory Allocation** (`alloc()`):
   - Traverses the heap to find a free block that is large enough to satisfy the memory request.
   - If a block is too large, it is split into two blocks, and the remaining part is added back to the free list.
   
4. **Memory Freeing** (`free_mem()`):
   - Marks a block as free and attempts to merge adjacent free blocks to reduce fragmentation.

5. **Memory Block Merging** (`merge_freeList()`):
   - Combines adjacent free blocks to form larger free blocks, reducing fragmentation.

6. **Heap Re-initialization** (`dealloc_heap()`):
   - Deallocates all memory blocks and reinitializes the heap.

7. **Print Heap Status** (`printList()`):
   - Displays all blocks in the heap, showing block sizes and whether they are free or allocated.
   - Displays the stored data if the block is allocated.

## How It Works

1. **Initialize the Heap**:
   The heap is initialized with a block of size 1024 bytes. You can allocate memory for different data types like integers, doubles, and strings.

2. **Memory Allocation**:
   The program uses a linked list of memory blocks to simulate memory allocation. When allocating memory, the heap is searched for a free block large enough to hold the requested size.

3. **Free Memory and Merge**:
   When a block is freed, it is marked as free and the adjacent free blocks are merged into a single larger block, reducing memory fragmentation.

4. **Print Heap Status**:
   You can view the current status of the heap, showing allocated and free blocks along with their sizes. If a block is allocated, its data is displayed.

## How to Use

### Compilation

To compile the program, use any C compiler like `gcc`:

```bash
gcc heap_manager.c -o heap_manager
```

### Running the Program

Once compiled, run the executable:

```bash
./heap_manager
```

### Program Workflow

1. The user is prompted to enter the maximum number of pointers.
2. The user is presented with the following options:
   - **1. Allocate integer value**: Allocate memory for an integer and store a value.
   - **2. Allocate double value**: Allocate memory for a double value and store it.
   - **3. Allocate string value**: Allocate memory for a string and store it.
   - **4. Print list**: Display the current state of the heap (block sizes and statuses).
   - **5. Free memory**: Free a specific memory block by specifying its index.
   - **6. Deallocate and re-initialize**: Deallocate the entire heap and reinitialize it.
   - **7. Merge free lists**: Merge adjacent free blocks to reduce memory fragmentation.

### Example

1. **Allocate Integer**:
   ```bash
   enter integer data value:
   42
   ```

2. **Allocate String**:
   ```bash
   enter string data:
   hello
   ```

3. **Print List**:
   Displays block sizes, allocation statuses, and stored data.

4. **Free Memory**:
   Frees a block at a specified index.

5. **Merge Free Lists**:
   Merges adjacent free memory blocks to reduce fragmentation.

## Example Output

```
Options:
1. Allocate integer value
2. Allocate double value
3. Allocate string value
4. Print list
5. Free memory
6. Deallocate and re-initilized
7. Merge free lists
Enter your choice: 1
enter integer data value:
10
Block: Size = 4, Allocated, Data = 10

Enter your choice: 3
enter string data:
Hello
Block: Size = 6, Allocated
Block: Size = 4, Allocated, Data = 10

Enter your choice: 4
Block: Size = 6, Allocated, Data = Hello
Block: Size = 4, Allocated, Data = 10
```

## Limitations

- The heap size is fixed at 1024 bytes.
- Does not handle reallocation (`realloc`).
- Pointers and memory blocks are managed manually, and improper use can lead to errors or segmentation faults.

## Future Improvements

- Add dynamic heap resizing.
- Implement support for floating-point numbers.
- Include more robust error handling for edge cases (e.g., trying to free a pointer that was not allocated).
