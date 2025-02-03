# Auto Keyword in C++

## Introduction
The `auto` keyword in C++ allows the compiler to automatically deduce the type of a variable at compile time. This is particularly useful for simplifying code and improving maintainability.

## Example 1: Basic Usage
```cpp
#include <iostream>
#include <string>

std::string getname() { return "cherno"; }

int main() {
    // Example 1: Auto infers the type from an integer
    int a = 10;
    auto b = a; // Here you can see auto keyword will automatically identify the data type.
}
```

## Example 2: Function Return Type Inference
```cpp
#include <iostream>
#include <string>

std::string getname() { return "cherno"; }

int main() {
    // Example 2: Auto infers type from function return
    auto name = getname(); 
    // Here both pro and con are available. Consider two sides: client and server.
    // Server side is `getname()`, main function is client side.
    // Client side uses `auto`. If we change `std::string` to `char`, `int`, `float` in the server side,
    // we don't need to change anything in the client side because `auto` adapts to any data type.
    // 
    // This is the con: We might lose track of expected types.
    // This is the pro: If we change `std::string` to `char`, in the client side we don’t need to update the code twice.
    // 
    // In most cases, use explicit data types. Use `auto` for long data types.
}
```

## Example 3: Auto with Long Datatypes (Iterator Example)
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    
    // Instead of writing std::vector<int>::iterator, we use auto
    auto it = numbers.begin();
    
    while (it != numbers.end()) {
        std::cout << *it << " ";
        ++it;
    }
}
```

### Explanation
- Here, `auto` deduces the iterator type (`std::vector<int>::iterator`) automatically.
- Makes code more readable and avoids typing long and complex type names.

### When to Use `auto`
✅ Use `auto` when dealing with long type names like iterators or complex templates.
✅ Use `auto` when the exact type is irrelevant to the logic.
❌ Avoid `auto` if it reduces code readability and clarity.

Hope this helps! 🚀
