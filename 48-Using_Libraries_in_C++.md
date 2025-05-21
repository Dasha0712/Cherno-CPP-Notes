# 📚 Using Libraries in C++ (Static Linking)

In C++, libraries provide reusable code in either **static** or **dynamic** formats. This guide focuses on **static linking**, where the library code is embedded directly into your executable at **compile time**.

---

## 🧱 What is Static Linking?

* Static linking **copies** all used code from the library into your executable.
* The final `.exe` contains **everything it needs** to run — no external files required.
* It allows for **better optimization** since the linker can see the full code.

---

## 🔗 Linking Libraries Statically

To use a library statically:

1. **Include header files** in your code (e.g. `#include <GLFW/glfw3.h>`)
2. **Link the static `.lib` file** in your project settings
3. **Ensure you define** any required preprocessor flags (e.g. `GLFW_STATIC`)

### Example with GLFW (Static Link)

```cpp
#include <GLFW/glfw3.h>

int main() {
    if (glfwInit()) {
        return 1;
    }
    return 0;
}
```

➡️ **Visual Studio Settings**:

```
Project Properties
├── C/C++
│   └── Preprocessor
│       └── Preprocessor Definitions: GLFW_STATIC
├── Linker
│   └── Input
│       └── Additional Dependencies: glfw3.lib
├── VC++ Directories
│   ├── Include Directories: (path to GLFW includes)
│   └── Library Directories: (path to GLFW .lib)
```

---

## ✅ Benefits of Static Linking

* Fewer external dependencies
* Easier deployment (1 executable)
* Potentially **faster performance** (due to inlining and optimization)

---

## ⚠️ Drawbacks

* Larger executable size
* Need to recompile every time the library changes
* Cannot switch versions at runtime

---

## 🔍 Summary Table

| Feature            | Static Linking  |
| ------------------ | --------------- |
| Link time          | Compile time    |
| Runtime dependency | ❌ None          |
| Executable size    | Larger          |
| Optimizations      | ✅ More possible |
| Flexibility        | ❌ Less flexible |

---

## 🧠 Final Notes

* Static linking is great for final release builds or tools where simplicity is preferred.
* For modular systems or large codebases, consider **dynamic linking** instead.

💡 Want to learn about **dynamic linking**? Check out the next guide!
