# Header Files in C++

## 🔹 What Are Header Files?

Header files in C++ allow us to declare functions, classes, structs, and other entities in one place and use them across multiple files. They're especially helpful for organizing code and enabling modular programming.

---

## 🔹 Why Use Header Files?

Imagine you have a function defined in `log.cpp` but you want to use it in `main.cpp`.
You must first tell the compiler that the function exists — this is called a **declaration**. Rather than declaring every function in every file manually, you can place all declarations in a **header file**, then just `#include` that header where needed.

---

## 🔹 Code Example: Using Header Files

### File 1: `main.cpp`

```cpp
#include "log.h"

int main() {
    initLog();
    return 0;
}
```

### File 2: `log.cpp`

```cpp
#include <iostream>
#include "log.h"

void log(const char* message) {
    std::cout << message << std::endl;
}

void initLog() {
    log("Logging initialized");
}
```

### File 3: `log.h`

```cpp
#pragma once

void log(const char* message);
void initLog();
```

This example shows how header files can centralize declarations and simplify code reuse.

---

## 🔹 What is `#pragma once`?

* `#pragma once` is a directive that ensures the file is included **only once** in each compilation unit.
* It prevents multiple definition errors.

### 🧪 Example: Duplicate Definitions Without `#pragma once`

#### `log.h`

```cpp
struct Player {
    int health;
};
```

#### `common.h`

```cpp
#include "log.h"  // This includes Player struct again
```

#### `main.cpp`

```cpp
#include "log.h"
#include "common.h"  // Player is included twice accidentally

int main() {
    Player p;
    p.health = 100;
}
```

This would cause a **duplicate symbol error** unless we use `#pragma once` in `log.h`.

---

## 🔹 `#include <...>` vs `#include "..."`

* `#include <filename>`: Used for **standard library headers** or compiler-specific include paths.
* `#include "filename"`: Used for **user-defined** or local files.

You can use `"filename"` for everything, but `<>` is recommended for system headers.

---

## 🔹 Extensions: `.h` vs No Extension

* In **C++**, standard library headers (like `<iostream>`, `<vector>`) typically **do not** have an extension.
* In **C**, standard headers usually have a `.h` extension (like `<stdio.h>`, `<math.h>`).
* Custom headers created by the user often use the `.h` extension (e.g., `log.h`).

---

## ✅ Summary

| Concept              | Purpose                           |
| -------------------- | --------------------------------- |
| Header File          | Centralize declarations           |
| `#pragma once`       | Prevent multiple inclusions       |
| `<>` vs `""`         | System vs user includes           |
| `.h` vs No Extension | C headers vs C++ standard headers |

Using header files properly makes your codebase more modular, reusable, and easier to maintain.
