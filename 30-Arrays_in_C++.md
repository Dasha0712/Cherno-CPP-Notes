# Arrays in C++

Welcome back to the C++ series! This note summarizes the key points from The Cherno's video on **Arrays in C++**, intended to be a clear and comprehensive reference.

## Prerequisite: Pointers
Before diving into arrays, make sure you understand **pointers** in C++. Arrays and pointers are closely related, and understanding pointers will make it much easier to grasp arrays.

## What is an Array?
- An array is a collection of **elements** of the same type.
- It allows storing multiple variables **under one name**, accessed by an **index**.
- Useful when dealing with large sets of data (e.g., storing 50 integers).

### Problem Without Arrays
Imagine needing 50 integer variables:
```cpp
int number1 = 0;
int number2 = 0;
// up to number50...
```
This is impractical and unmaintainable.

## Declaring an Array
```cpp
int example[5];
```
This creates an array named `example` with 5 integers.

## Accessing Elements
```cpp
example[0] = 2; // first element
example[4] = 4; // fifth element
```
- Index starts from 0.
- Accessing index outside range (like `example[5]` or `example[-1]`) causes **memory access violations**.

## Reading Elements
```cpp
int x = example[2]; // x gets value of third element
```

## Printing an Array
- `cout << example;` prints the memory address (not contents).
- Use a loop to access and print each element.

## For Loop with Arrays
```cpp
for (int i = 0; i < 5; i++) {
    example[i] = 2;
}
```

## Memory Representation
- Arrays are stored **contiguously** in memory.
- Each `int` takes 4 bytes.
- Accessing an element calculates the offset:
  - `example[2]` → offset `2 * sizeof(int)` = 8 bytes from base address.

## Pointers and Arrays
```cpp
int* pointer = example;
pointer[2] = 6;
```
Same as:
```cpp
*(pointer + 2) = 6;
```

## Advanced Pointer Arithmetic
```cpp
*((int*)((char*)pointer + 8)) = 6;
```
This manually shifts memory by 8 bytes and casts back to `int*`.

## Stack vs Heap Allocation
### Stack Array
```cpp
int example[5];
```
- Automatically destroyed when scope ends.

### Heap Array
```cpp
int* another = new int[5];
delete[] another; // Manual deallocation required
```

## Standard Array (`std::array`)
- Introduced in C++11.
- Provides bounds checking, size tracking.
- Example:
```cpp
#include <array>
std::array<int, 5> example = {2, 2, 2, 2, 2};
```

## Getting Array Size
### Stack Array
```cpp
int array[5];
int size = sizeof(array) / sizeof(int); // gives 5
```

### Heap Array
```cpp
int* heapArray = new int[5];
int size = sizeof(heapArray) / sizeof(int); // gives wrong result (1 or 0)
```
- You must track heap array size manually.

## Best Practices
- Use `const int SIZE = 5;` for array size constants.
- For stack arrays, size must be **compile-time constant**.

---

Arrays are a foundational concept in C++. Understanding how memory works with arrays, how indexing and pointers interact, and how stack vs heap affects behavior is critical for writing efficient and safe code.