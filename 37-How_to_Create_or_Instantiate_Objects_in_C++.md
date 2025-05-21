# How to Create / Instantiate Objects in C++

In C++, once we define a class, we usually want to create and use objects of that class. C++ provides two primary ways to create (instantiate) objects:

1. **On the Stack**
2. **On the Heap**

The difference lies in where the memory for the object is allocated and how it is managed.

---

## What is Scope?

**Scope** refers to the region of the code where a variable or object exists and can be accessed. When a variable goes **out of scope**, it is automatically destroyed (in the case of stack allocation).

Scopes can be defined by:

* Functions
* Loops (`for`, `while`, etc.)
* Conditional blocks (`if`, `else`, etc.)
* Custom `{}` blocks (anonymous scopes)

```cpp
{
    int x = 5; // x is valid within these braces
} // x goes out of scope and is destroyed here
```

---

## Example Class Definition

Let's define a simple class named `Entity` outside the `main` function:

```cpp
#include <iostream>
#include <string>

using String = std::string;

class Entity {
private:
    String m_Name;

public:
    Entity() : m_Name("Unknown") {}
    Entity(const String& name) : m_Name(name) {}

    const String& GetName() const { return m_Name; }
};
```

This class has:

* A private member variable `m_Name`
* A default constructor that initializes `m_Name` to "Unknown"
* A parameterized constructor
* A getter method `GetName()`

---

## Creating Objects on the Stack

Stack allocation is straightforward and efficient. The object is automatically destroyed when it goes out of scope.

```cpp
int main() {
    Entity entity1;                     // Calls default constructor
    Entity entity2("Cherno");          // Calls parameterized constructor

    std::cout << entity1.GetName() << std::endl; // Outputs: Unknown
    std::cout << entity2.GetName() << std::endl; // Outputs: Cherno

    return 0;
} // entity1 and entity2 go out of scope here
```

---

## Creating Objects on the Heap

Heap allocation gives you control over the lifetime of the object, but **you must delete the object manually** to prevent memory leaks.

```cpp
int main() {
    Entity* entity = new Entity("Cherno");
    std::cout << entity->GetName() << std::endl; // Outputs: Cherno

    delete entity; // Manual cleanup is required
    return 0;
}
```

Using `new` allocates memory on the heap. The object will not be destroyed until you call `delete`.

---

## When to Use Stack vs Heap

| Stack                          | Heap                                |
| ------------------------------ | ----------------------------------- |
| Automatic lifetime             | Manual lifetime management          |
| Faster allocation/deallocation | Slower, but more flexible           |
| Limited in size (\~1MB–2MB)    | Suitable for large objects          |
| No memory leaks                | Risk of memory leaks if not deleted |

**Use stack allocation** whenever possible. Use heap only if:

* You need the object to outlive its scope.
* The object is too large to fit on the stack.

---

## Common Mistake: Dangling Pointers

Never return a pointer or reference to a local (stack-allocated) variable:

```cpp
Entity* GetEntity() {
    Entity e("Invalid");
    return &e; // Dangerous! e is destroyed when function exits
}
```

---

## Smart Pointers (Mentioned Briefly)

In modern C++, it's recommended to use smart pointers like `std::unique_ptr` and `std::shared_ptr` to manage heap memory safely. This avoids manual `delete` calls.

---

## Summary

* Use stack allocation for simplicity, performance, and automatic cleanup.
* Use heap allocation only when necessary, and remember to `delete`.
* Understand **scope** to avoid dangling pointers and memory issues.

Next: We will explore the `new` keyword in more detail.