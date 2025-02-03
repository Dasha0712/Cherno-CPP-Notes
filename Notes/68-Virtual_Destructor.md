## Why Use a Virtual Destructor in C++ Inheritance?

### Problem: Memory Leak Without a Virtual Destructor

When using **inheritance** in C++, the base class destructor should be declared **virtual** to ensure proper cleanup of derived class objects. Otherwise, if a base class pointer is used to delete a derived class object, the derived class's destructor **will not be called**, causing a **memory leak**.

### Example: Incorrect Usage Without Virtual Destructor

```cpp
#include <iostream>

class Base {
public:
    Base() { std::cout << "Base constructor" << std::endl; }
    ~Base() { std::cout << "Base destructor" << std::endl; }
};

class Derived : public Base {
private:
    int* m_array;

public:
    Derived() {
        m_array = new int[5];  // Allocating memory on the heap
        std::cout << "Derived constructor" << std::endl;
    }
    ~Derived() {
        delete[] m_array;  // Memory should be released here
        std::cout << "Derived destructor" << std::endl;
    }
};

int main() {
    Base* base = new Base();
    delete base;  // Correctly calls Base destructor
    
    std::cout << "------------------------\n" << std::endl;
    
    Derived* derived = new Derived();
    delete derived;  // Correctly calls Derived destructor
    
    std::cout << "------------------------\n" << std::endl;
    
    Base* poly = new Derived();
    delete poly;  // INCORRECT: Derived destructor is NOT called, causing memory leak
    
    std::cout << "------------------------\n" << std::endl;
}
```

### Issue Explained:
- **Base class destructor is NOT virtual**, so when deleting `poly`, only `Base`'s destructor runs, skipping `Derived`'s destructor.
- This causes `m_array` **not to be deleted**, leading to **a memory leak**.

---

### Solution: Use a Virtual Destructor

To fix this issue, declare the **base class destructor as virtual** so that the derived class destructor is correctly called when an object is deleted through a base class pointer.

```cpp
#include <iostream>

class Base {
public:
    Base() { std::cout << "Base constructor" << std::endl; }
    virtual ~Base() { std::cout << "Base destructor" << std::endl; }  // Virtual destructor ensures proper cleanup
};

class Derived : public Base {
private:
    int* m_array;

public:
    Derived() {
        m_array = new int[5];  // Allocating memory on the heap
        std::cout << "Derived constructor" << std::endl;
    }
    ~Derived() {
        delete[] m_array;  // Properly releasing allocated memory
        std::cout << "Derived destructor" << std::endl;
    }
};

int main() {
    Base* base = new Base();
    delete base;  // Base destructor is called
    
    std::cout << "------------------------\n" << std::endl;
    
    Derived* derived = new Derived();
    delete derived;  // Derived destructor is correctly called
    
    std::cout << "------------------------\n" << std::endl;
    
    Base* poly = new Derived();
    delete poly;  // CORRECT: Base destructor is virtual, so Derived destructor is called first, preventing memory leak
    
    std::cout << "------------------------\n" << std::endl;
}
```

### Key Takeaways:
✅ Always declare **virtual destructors** in base classes when using **polymorphism**.
✅ A **virtual destructor ensures proper cleanup** of derived class objects.
✅ **Forgetting a virtual destructor can lead to memory leaks** when using base class pointers.

This is an important concept in C++ for managing dynamic memory correctly! 🚀
