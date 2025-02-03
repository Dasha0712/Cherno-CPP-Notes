# Understanding C++ Standard Arrays vs C-Style Arrays

This example explains the usage of standard arrays (`std::array`) and compares them with traditional C-style arrays.

---
## **Code Example:**

```cpp
#include <iostream>
#include <array>

void printArray(const std::array<int, 5>& data) {
    // Efficient way to iterate using size() method of std::array
    for (int i = 0; i < data.size(); i++) {
        std::cout << data[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    // **New Model: Standard Array**
    std::array<int, 5> array_name;
    array_name[0] = 99;
    array_name[2] = 100;

    // Print using the function
    printArray(array_name);

    // **Old C-Style Model**
    int array_name1[4];
    array_name1[0] = 69;

    // Display a C-style array example
    std::cout << "C-Style Array: " << array_name1[0] << std::endl;
}
```

---
### **Key Differences:**

1. **C-Style Arrays:**
   - Fixed-size memory on the stack.
   - Manual size tracking; you must pass the size as a separate argument when processing arrays.
   - No built-in functions for operations like size or bounds checking.

2. **Standard Arrays (`std::array`)**:
   - Also stored on the stack for optimized access.
   - Size is part of the type (using templates), so no separate memory is required for size tracking.
   - Provides member functions like `size()`, making it easier to work with.

### **Why Use `std::array`:**
- Safer than C-style arrays due to built-in bounds checking functions.
- Template-based size eliminates the need for separate memory for size tracking.
- You can view the implementation by exploring the standard library header file for detailed insights.

By understanding and utilizing `std::array`, your C++ programs will be more robust and easier to maintain.

