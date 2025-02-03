# Threads in C++

## Introduction
Multithreading is a powerful feature in C++ that allows multiple threads to run concurrently, improving performance and responsiveness. The `std::thread` library provides a simple way to create and manage threads in C++.

---

## Understanding Threads
A thread is a lightweight process that runs independently within a program. Multiple threads can execute different tasks simultaneously, utilizing multi-core processors efficiently. 

### Key Concepts:
- **Thread Creation:** `std::thread` is used to create a new thread.
- **Thread Synchronization:** Ensuring threads work correctly without data races.
- **Thread Joining (`join()`):** The main thread waits for the created thread to finish execution.
- **Thread Sleep (`sleep_for()`):** A thread can be paused for a specified duration.

---

## Example: Implementing a Thread in C++
```cpp
#include <iostream>
#include <thread>
using namespace std::literals::chrono_literals;

static bool cond = false;

void printsomething() {
    std::cout << "Thread ID: " << std::this_thread::get_id() << std::endl;
    while (!cond) {
        std::cout << "Waiting..." << std::endl;
        std::this_thread::sleep_for(1s); // Sleep for 1 second
    }
}

int main() {
    std::thread t(printsomething); // Create a new thread
    std::cin.get(); // Wait for user input
    cond = true; // Condition to stop waiting

    t.join(); // Main thread waits for 't' to complete
    std::cout << "Finished!" << std::endl;
    std::cout << "Main Thread ID: " << std::this_thread::get_id() << std::endl;
    
    std::cin.get(); // Wait before closing the program
}
```

---

## Explanation of the Code
1. **Thread Creation:**
   - `std::thread t(printsomething);` creates a new thread that runs the `printsomething` function.
   - This function prints the thread ID and waits until `cond` becomes `true`.

2. **Thread Sleep:**
   - `std::this_thread::sleep_for(1s);` pauses execution for 1 second to simulate waiting.

3. **Thread Synchronization:**
   - The main thread waits for user input (`std::cin.get();`).
   - After pressing Enter, `cond` becomes `true`, signaling the thread to exit the loop.

4. **Thread Joining:**
   - `t.join();` ensures the main thread waits until the created thread (`t`) completes its execution.

5. **Thread IDs:**
   - `std::this_thread::get_id();` prints each thread’s unique ID to show that the main thread and `t` have different IDs.

---

## Summary Table
| Feature | Description |
|---------|-------------|
| `std::thread` | Creates a new thread |
| `std::this_thread::sleep_for(duration)` | Pauses a thread for a given time |
| `join()` | Waits for a thread to complete |
| `std::this_thread::get_id()` | Gets the current thread’s unique ID |

---

## Conclusion
Threads in C++ help in parallel execution, improving performance and efficiency. However, proper synchronization is crucial to avoid race conditions and deadlocks. Use `join()` to ensure threads complete their execution before the main thread terminates.

---

This structured approach makes the concept of threads easy to revisit and understand, even after months! 🚀

