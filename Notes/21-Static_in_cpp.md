# C++ Example: Static and External Variables

This example illustrates the use of `static` and `extern` keywords in C++ and how they affect variable linkage.

---
## **Code Example**

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl

// int variable = 100;
extern int variable;
// static int variable = 100;

int main() {
    print(variable);
}
```

---
## **Explanation:**

### **Variable Definitions:**
1. `int variable = 100;`: This creates a global variable.
2. `static int variable = 100;`: A static variable has internal linkage, meaning it is only accessible within the file where it is defined.
3. `extern int variable;`: This tells the linker to search for the definition of `variable` in another file.

### **Problem:**
In the original code, there were two potential definitions for `variable` (global and static). The linker wouldn't know which definition to choose, causing an error.

### **Solutions:**
1. **Use `extern` Keyword:**
   By using `extern`, the linker will look for the definition of `variable` in another file.

2. **Make `variable` Static:**
   By declaring `variable` as `static`, it becomes confined to the current file, resolving any ambiguity for the linker.

### **Key Notes:**
- Use `extern` when you want to share a variable across multiple files.
- Use `static` for file-specific variables to avoid naming conflicts.

By understanding these concepts, you can better manage variable scope and linkage in your C++ programs.

