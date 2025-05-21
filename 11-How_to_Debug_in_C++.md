# How to Debug in C++ (Cherno Notes)

## Why Debugging is Important

* Debugging helps you **understand how programs and computers actually work**.
* It's essential not only to fix bugs but also to **learn programming deeply**.
* The computer is almost always right; bugs are usually the **programmer's mistake**.

---

## Key Concepts

* **Breakpoints**: Pause execution at specific lines to inspect program state.
* **Reading Memory**: Check what data is stored at runtime in variables and memory.

---

## Tools Used

* **IDE**: Visual Studio (concepts apply to most IDEs)
* **View Windows**:

  * **Autos** and **Locals**: Automatically populated with relevant variables.
  * **Watch**: Manually monitor specific variables.
  * **Memory View**: View raw memory data.

---

## Setting Breakpoints

### Ways to Set:

* Press `F9` on the line.
* Click in the left margin next to the code line.

> ⚠️ Set breakpoints on lines that contain **executable code**, not empty lines or comments.

### Run the Debugger

* Make sure you're in **Debug Mode**, not Release Mode.
* Click `Local Windows Debugger` (or press `F5`).

> 📌 In **Release Mode**, the compiler may rearrange or optimize code, preventing breakpoints from working as expected.

---

## Debugger Interface Overview

### On Breakpoint Hit:

* The editor shows a **yellow arrow** at the paused line (not yet executed).
* You can hover over variables to inspect values.

### Controls:

* **Continue (`F5`)**: Resume program execution.
* **Step Into (`F11`)**: Go inside the current function.
* **Step Over (`F10`)**: Execute the current line and move to the next.
* **Step Out (`Shift+F11`)**: Exit the current function and return to the caller.

---

## Example Code for Debugging

```cpp
int main() {
    int a = 8;
    a++;
    const char* string = "hello";

    for (int i = 0; i < 5; i++) {
        char c = string[i];
        std::cout << c << std::endl;
    }

    Log("Hello World");
}
```

---

## Inspecting Variables

* At a breakpoint, hover over variables to see current values.
* Use the **Watch Window**:

  * Add variable names (e.g., `a`, `string`) to monitor their values.
* You can also view **uninitialized variables** to see raw memory (garbage values).

---

## Memory View

### Steps:

1. Go to `Debug > Windows > Memory > Memory 1`.
2. Use `&a` in the memory view to see where variable `a` is stored.

### Example:

* Uninitialized memory might show as `0xCC`, meaning uninitialized **stack memory**.
* In Debug Mode, the compiler **fills uninitialized stack memory** with `0xCC` to help spot issues.

### Convert Hex to Decimal:

* Use Windows Calculator → Programmer Mode → Hex to Dec conversion.

---

## Using the Watch Window

* Right-click in Watch → Toggle `Hexadecimal Display` to view hex values.
* `a` before execution: might show as garbage (`0xCCCCCCCC`).
* `a` after `a = 8;` will update to `8`.

> ✅ Updated variables in Watch appear in **red** to indicate a change.

---

## Tracking Changes in Memory

* After initializing a variable:

  * Memory view will reflect the actual bytes used.
  * E.g., `8` becomes `0x08` in the corresponding memory bytes.

---

## Strings in Memory

* After initializing `const char* string = "hello";`, the Watch window shows the address.
* Use that address in Memory View to see:

  * **ASCII characters** on the right ("hello").
  * Strings like `"Stack around the variable was corrupted"` in memory (for debug help).

> 🚫 These debug strings won't appear in **Release Mode**.

---

## Debugging Loops

* Step through `for` loop iterations using `F10`.
* Inspect loop variables like `i`, `c`.
* Watch variable `c` update with each iteration.

### Example:

```cpp
for (int i = 0; i < 5; i++) {
    char c = string[i];
    std::cout << c << std::endl;
}
```

* Use Watch to observe values of `c`, `i`.
* Use `&c` to see the memory location of `c`.

---

## Skipping Code in Loops

* Want to **exit a loop early** or skip stepping through it?

  * Set a breakpoint **after** the loop.
  * Hit `F5` to continue execution until that point.

---

## Summary

* Use breakpoints to pause execution.
* Step through code using `F10`, `F11`, `Shift+F11`.
* Read memory and variable values in **Watch**, **Autos**, **Locals**.
* Use **Memory View** for deep inspection.
* Debug Mode fills memory with helpful patterns (`0xCC`) to identify issues.
* Avoid debugging in Release Mode unless necessary.

> 💡 Mastering debugging tools helps you better understand code execution and memory management in C++.
