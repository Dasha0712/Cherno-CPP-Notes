# Function Pointer Aliases in C++

There are two primary methods for creating aliases for function pointer types in C++: using the `auto` keyword and using `typedef`. Below are examples for both methods:

---
## **Method 1: Using `auto` Keyword**
This method simplifies defining function pointers by leveraging the `auto` keyword.

```cpp
#include <iostream>

void helloworld() {
    std::cout << "Hello, World!" << std::endl;
}

int main() {
    // `auto` infers the type as `void(*function_name)()`
    auto function_name = helloworld;
    // Equivalent: auto function_name = &helloworld;

    // Call the function via the pointer
    function_name();
    function_name();
}
```
### **Notes:**
- The `auto` keyword automatically infers the type `void(*function_name)()`.
- No need to use the `&` symbol to take the address of the function explicitly.

---
## **Method 2: Using `typedef`**
This is a traditional approach where `typedef` defines a function pointer type.

### **Syntax:**
```cpp
typedef ReturnType (*NewTypeName)(ParameterType1, ParameterType2, ...);
```

### **Example:**
```cpp
#include <iostream>

void helloworld(int x) {
    std::cout << "Hello, World! " << x << std::endl;
}

int main() {
    // Define a function pointer type using typedef
    typedef void(*function_name)(int);

    function_name fn = helloworld;

    // Call the function via the pointer
    fn(90);
    fn(100);
}
```
### **Notes:**
- `typedef void(*function_name)(int);` defines `function_name` as a type for pointers to functions taking an `int` and returning `void`.
- Cherno prefers using the `typedef` method in his examples.

---
### **Why Use Function Pointers?**
Function pointers enable dynamic function calls, useful for callbacks, event handling, and scenarios requiring polymorphism in non-OOP designs.

By mastering both methods, you gain flexibility and clarity in writing cleaner and more maintainable C++ code.

