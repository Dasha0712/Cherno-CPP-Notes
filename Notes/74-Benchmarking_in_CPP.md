# Benchmarking

## Timer Class: Measuring Execution Time
The `Timer` class is used to measure the execution time of a code block. It starts a timer when an object is created and stops it when the object is destroyed (RAII principle). 

### **Code Explanation**
```cpp
#include<iostream>
#include<memory>
#include <chrono>

class Timer
{
private:
    std::chrono::time_point<std::chrono::high_resolution_clock> m_StartTimepoint;
public:
    Timer()
    {
        m_StartTimepoint = std::chrono::high_resolution_clock::now();
    }
    ~Timer()
    {
        Stop();
    }
    void Stop()
    {
        auto endpoint = std::chrono::high_resolution_clock::now();

        auto start = std::chrono::time_point_cast<std::chrono::microseconds>(m_StartTimepoint).time_since_epoch().count();
        auto stop = std::chrono::time_point_cast<std::chrono::microseconds>(endpoint).time_since_epoch().count();

        auto duration = stop - start;
        double ms = duration * 0.001;
        std::cout << duration << "us (" << ms << "ms)\n";
    }
};

int main()
{
    int value = 0;
    {
        Timer timer; // Timer starts here, stops when scope ends
        for(int i = 0; i < 100000; i++)
            value += 2;
    }
    std::cout << value << std::endl;

    __debugbreak(); // Windows-specific debug breakpoint
}
```

### **Breakdown of the Code**
- `std::chrono::high_resolution_clock::now();` → Captures the current time.
- `std::chrono::time_point_cast<std::chrono::microseconds>` → Converts time to microseconds.
- `duration * 0.001` → Converts microseconds to milliseconds.
- The `Timer` object starts counting in the constructor and automatically stops when it goes out of scope.
- `__debugbreak();` → A Windows-only command that acts as a breakpoint.

---

## **Unique Pointer vs Shared Pointer: Performance Comparison**

### **Unique Pointer (`std::unique_ptr`)**
- Manages a single object exclusively.
- When it goes out of scope, the memory is automatically freed.
- Faster than `shared_ptr` since no reference counting is required.
- Best used when you want **exclusive ownership** of an object.

#### **Example Usage of Unique Pointer**
```cpp
#include <iostream>
#include <memory>

class UniqueExample {
public:
    UniqueExample() { std::cout << "UniqueExample Created\n"; }
    ~UniqueExample() { std::cout << "UniqueExample Destroyed\n"; }
};

int main() {
    std::unique_ptr<UniqueExample> ptr = std::make_unique<UniqueExample>();
    return 0;
}
```
✅ **Use when:** You want a **single owner** for an object.

---

### **Shared Pointer (`std::shared_ptr`)**
- Allows multiple shared ownerships of an object.
- Uses reference counting, which slightly impacts performance due to extra overhead.
- Best used when multiple parts of your program **must share ownership** of an object.

#### **Example Usage of Shared Pointer**
```cpp
#include <iostream>
#include <memory>

class SharedExample {
public:
    SharedExample() { std::cout << "SharedExample Created\n"; }
    ~SharedExample() { std::cout << "SharedExample Destroyed\n"; }
};

void Function(std::shared_ptr<SharedExample> ptr) {
    std::cout << "Inside Function\n";
}

int main() {
    std::shared_ptr<SharedExample> ptr = std::make_shared<SharedExample>();
    Function(ptr);
    return 0;
}
```
✅ **Use when:** Multiple parts of the code need access to the same object **without manually managing memory**.

---

### **Performance Measurement**
```cpp
#include <iostream>
#include <memory>
#include <chrono>

void UniquePtrTest()
{
    Timer timer;
    for (int i = 0; i < 1000000; i++)
    {
        std::unique_ptr<int> ptr = std::make_unique<int>(i);
    }
}

void SharedPtrTest()
{
    Timer timer;
    for (int i = 0; i < 1000000; i++)
    {
        std::shared_ptr<int> ptr = std::make_shared<int>(i);
    }
}

int main()
{
    std::cout << "Unique Pointer Performance: " << std::endl;
    UniquePtrTest();
    
    std::cout << "Shared Pointer Performance: " << std::endl;
    SharedPtrTest();
}
```

### **Expected Output**
- Unique pointers should perform faster because they don't use reference counting.
- Shared pointers involve overhead due to reference counting, making them slightly slower.

---

## **Final Thoughts**
- Use `std::unique_ptr` when ownership isn't shared.
- Use `std::shared_ptr` when multiple parts of the program need access to an object.
- Use RAII (Resource Acquisition Is Initialization) techniques, like the `Timer` class, to ensure resource cleanup automatically.

Would you like further improvements or additional examples?
