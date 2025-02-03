# Understanding Stack and Heap Allocation in C++

## 1. Normal Values

### Stack Allocation
```cpp
int s_value = 1;
```
- **Stored in Stack**
- Memory is automatically managed

### Heap Allocation
```cpp
int* h_value = new int;
*h_value = 90;
```
- **Stored in Heap**
- Requires manual memory management (`delete` required but missing in this code)

## 2. Arrays

### Stack Allocation
```cpp
int s_array[20];
```
- **Stored in Stack**
- Automatically deallocated

### Heap Allocation
```cpp
int* h_array = new int[20];
```
- **Stored in Heap**
- Needs manual deallocation using `delete[] h_array;`

## 3. Class and Struct

### Stack Allocation
```cpp
vector s_vector2d;
```
- **Stored in Stack**
- Automatically deallocated

### Heap Allocation
```cpp
vector* h_vector2d = new vector;
```
- **Stored in Heap**
- Needs manual deallocation using `delete h_vector2d;`

---
## Debugging Stack and Heap in Visual Studio

To visualize memory allocation:
1. Set **breakpoints**
2. Go to **Debug → Windows → Memory → Memory1**
3. Observe:
   - **How stack allocates memory:** Stack grows downwards, and each function call creates a new stack frame. Local variables are stored in these frames and automatically removed when the function returns.
   - **How heap allocates memory:** The heap is managed by the OS and allocates memory dynamically as requested using `new`. This memory remains allocated until explicitly freed using `delete`.

> Both stack and heap allocations occur in **RAM**.

---
## Stack vs Heap Memory in C++

### Stack Memory

#### Definition:
A region of memory that stores local variables and function call information.

#### Characteristics:
- **Automatic Allocation:** Memory is automatically allocated and deallocated when functions are called and return.
- **Fixed Size:** Typically limited in size, which can lead to stack overflow if exceeded.
- **Fast Access:** Due to its structured nature, accessing stack memory is faster.

#### Usage:
Ideal for storing local variables, function parameters, and control flow data.

### Heap Memory

#### Definition:
A region of memory used for dynamic memory allocation, managed manually by the programmer.

#### Characteristics:
- **Manual Allocation:** Memory is allocated and deallocated using operators like `new` and `delete`.
- **Variable Size:** Can grow or shrink during runtime, limited by the system's available memory.
- **Slower Access:** Accessing heap memory can be slower due to its unstructured nature.

#### Usage:
Suitable for data that needs to persist beyond the scope of a function or for large data structures.

### Key Differences

- **Lifetime:** Stack variables have a limited lifetime, tied to the function scope, whereas heap variables persist until explicitly deallocated.
- **Management:** Stack memory is managed automatically, while heap memory requires manual management, increasing the risk of memory leaks.
- **Performance:** Stack operations are generally faster due to their predictable structure, whereas heap operations can be slower and may lead to fragmentation.

Understanding these differences is crucial for effective memory management in C++ programming, ensuring efficient and error-free code.

---
### Future Note
Use **Visual Studio debugging tools** to explore how memory is allocated and managed for stack and heap variables, arrays, and objects.
