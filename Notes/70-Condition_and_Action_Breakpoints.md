# **Debugger Breakpoints in C++**

When debugging C++ programs, breakpoints help stop code execution at specific points to inspect variables and program flow. Two important types of breakpoints are:

- **Conditional Breakpoints**
- **Action Breakpoints**

---

## **1. Conditional Breakpoints**
A **conditional breakpoint** is a breakpoint that pauses execution **only when a specified condition is met**. This is useful for stopping execution **only when a bug-triggering condition occurs**, instead of stopping every time.

### **Example: Stop only when `x == 5`**
```cpp
#include <iostream>

int main() {
    for (int x = 0; x < 10; x++) {
        std::cout << "Current value: " << x << std::endl;
    }
    return 0;
}
```
**How to set a conditional breakpoint:**
1. Place a breakpoint inside the `for` loop.
2. Set the condition to `x == 5`.
3. The debugger will **only stop when `x` is 5**, skipping other values.

✅ Useful when debugging loops or when an error happens under specific conditions.

---

## **2. Action Breakpoints**
An **action breakpoint** does not necessarily stop execution. Instead, it performs an action when hit, such as printing a message to the console. 

### **Two Types of Action Breakpoints:**
1. **Program runs after hitting the breakpoint** → Logs a message but doesn’t pause execution.
2. **Program pauses after hitting the breakpoint** → Allows inspection of variables before resuming execution.

### **Example: Print a message when a condition is met**
```cpp
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        std::cout << "Loop iteration: " << i << std::endl;
    }
    return 0;
}
```
**How to set an action breakpoint:**
1. Place a breakpoint inside the `for` loop.
2. Set an action like `Print "i is now: " + i`.
3. The program will print this message each time the breakpoint is hit **without pausing execution** (unless configured to do so).

✅ Useful when tracking values **without stopping the program every time**.

---

## **Summary**
| Type of Breakpoint | Purpose | Stops Execution? |
|--------------------|---------|-----------------|
| **Conditional Breakpoint** | Stops only when a condition is met | ✅ Yes |
| **Action Breakpoint (Log Only)** | Prints/logs a message when hit | ❌ No |
| **Action Breakpoint (Pause)** | Stops execution and allows inspection | ✅ Yes |

Using **conditional and action breakpoints** efficiently can **save debugging time** by focusing on **critical issues** instead of stopping execution unnecessarily.

---

### ✅ **Final Tip:**
- Use **conditional breakpoints** when debugging loops or specific error cases.
- Use **action breakpoints** to log values without stopping execution.

By mastering these, you can debug C++ programs **faster and more effectively!** 🚀
