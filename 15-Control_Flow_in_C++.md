# Control Flow in C++ (continue, break, return)

Control flow in C++ determines the order in which individual statements, instructions, or function calls are executed. Three essential control flow statements in C++ are `continue`, `break`, and `return`. Let's explore each of these in detail.

---

## 1. `break` Statement

### Purpose:

The `break` statement is used to terminate the nearest enclosing loop (`for`, `while`, or `do-while`) or `switch` statement prematurely.

### Syntax:

```cpp
break;
```

### Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 1; i <= 10; ++i) {
        if (i == 5) {
            break; // Exit the loop when i == 5
        }
        cout << i << " ";
    }
    return 0;
}
```

**Output:**

```
1 2 3 4
```

### When to Use:

* When a specific condition is met and you want to stop looping.
* In `switch` statements to prevent fall-through between cases.

---

## 2. `continue` Statement

### Purpose:

The `continue` statement skips the current iteration of the loop and proceeds with the next iteration.

### Syntax:

```cpp
continue;
```

### Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 1; i <= 5; ++i) {
        if (i == 3) {
            continue; // Skip the rest of the loop when i == 3
        }
        cout << i << " ";
    }
    return 0;
}
```

**Output:**

```
1 2 4 5
```

### When to Use:

* To skip over specific conditions inside loops.
* When you want to continue looping but skip executing certain parts for specific iterations.

---

## 3. `return` Statement

### Purpose:

The `return` statement ends the execution of a function and optionally returns a value to the caller.

### Syntax:

```cpp
return;       // Used in functions with void return type
return value; // Used in functions with a return type (e.g., int, float, etc.)
```

### Example:

```cpp
#include <iostream>
using namespace std;

int square(int x) {
    return x * x; // Return the square of x
}

int main() {
    int num = 5;
    cout << "Square of " << num << " is " << square(num) << endl;
    return 0;
}
```

**Output:**

```
Square of 5 is 25
```

### When to Use:

* To return a result from a function.
* To exit early from a function when a condition is met.

---

## Summary

| Statement  | Description                                     | Use Case Example                            |
| ---------- | ----------------------------------------------- | ------------------------------------------- |
| `break`    | Exits a loop or `switch` statement              | Stop looping when a condition is met        |
| `continue` | Skips to the next loop iteration                | Skip specific iteration inside a loop       |
| `return`   | Exits a function and optionally returns a value | Return result from a function or exit early |

Understanding and mastering these control flow tools is essential for writing clear and efficient C++ programs.
