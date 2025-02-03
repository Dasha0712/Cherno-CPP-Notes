# How to Store Any Data in C++

## Introduction
C++ provides multiple ways to store different types of data in a single variable, such as `std::any` and `std::variant`. Understanding the differences between them helps in deciding which one to use in different scenarios.

---

## Example Code: Using `std::any`
```cpp
#include <iostream>
#include <any>

int main()
{
    std::any data;
    
    // Storing an integer
    data = 2;
    std::cout << "Stored an integer: " << std::any_cast<int>(data) << std::endl;
    
    // Storing a string
    data = std::string("cherno");
    std::cout << "Stored a string: " << std::any_cast<std::string>(data) << std::endl;

    return 0;
}
```

---

## Explanation
1. `std::any` can hold any type of data, and its type can change at runtime.
2. `std::any_cast<T>(data)` extracts the stored value, but you must ensure it holds the correct type.
3. If you store a new value, the previous one is lost.

---

## Difference Between `std::any` and `std::variant`

| Feature       | `std::any`                           | `std::variant`                         |
|--------------|----------------------------------|----------------------------------|
| Type Safety  | No compile-time type safety    | Type-safe at compile-time       |
| Type Checking | Checked at runtime using `std::any_cast` | Checked at compile-time        |
| Multiple Types | Can store any type, even non-default constructible ones | Limited to predefined types     |
| Performance  | Slightly slower due to runtime type checking | Faster as types are known at compile time |

---

## When to Use `std::any`
- When the type of data is unknown at compile time.
- When you need maximum flexibility for storing different types.
- Suitable for dynamic configurations and scripting.

## When to Use `std::variant`
- When you know all possible types at compile time.
- When you need better performance with type safety.
- When implementing state machines or handling multiple known types.

---

## Additional Example: Using `std::any` with Type Checking
```cpp
#include <iostream>
#include <any>

int main()
{
    std::any data = 42;
    
    if (data.type() == typeid(int)) {
        std::cout << "Data contains an integer: " << std::any_cast<int>(data) << std::endl;
    } else {
        std::cout << "Data contains a different type" << std::endl;
    }
    
    return 0;
}
```

This approach ensures that we only attempt to extract data if we are certain of its type.

---

For more details, refer to the [cppreference documentation](https://en.cppreference.com/w/cpp/utility/any).

