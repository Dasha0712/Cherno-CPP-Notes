## Dynamic Libraries in C++ (Dynamic Linking)

Dynamic linking is a method of linking libraries at runtime, rather than at compile time like static linking. This approach has different performance implications, use cases, and configurations.

### 🔁 Difference Between Static and Dynamic Linking

* **Static Linking:**

  * Occurs at compile time.
  * The library code becomes part of the final binary.
  * Can lead to larger executables but allows for more optimization.
* **Dynamic Linking:**

  * Occurs at runtime.
  * External libraries (DLLs) are loaded into memory when the executable runs.
  * Smaller executable sizes but requires correct DLL setup.

### 🔍 When to Use Dynamic Linking

* When you want to:

  * Reduce executable size.
  * Update libraries independently.
  * Share a library between multiple applications.

---

### 🧪 Linking GLFW Dynamically (Example)

We’ll link the GLFW library dynamically instead of statically.

```cpp
#include <GLFW/glfw3.h>
```

This include remains the same whether you're using static or dynamic linking.

➡️ **Visual Studio Project Settings**:

➡️ **General > Additional Include Directories**

```
[path_to_glfw_include]
```

➡️ **Linker > Input > Additional Dependencies**

```
glfw3dll.lib
```

➡️ **Linker > General > Additional Library Directories**

```
[path_to_glfw_lib]
```

### 📦 Required Files

Make sure these files are correctly set up:

* `glfw3.dll` (place it next to your `.exe` or in a known search path)
* `glfw3dll.lib` (linked at compile time to provide references to the DLL)

### ⚠️ DLL Missing Error

If you see an error like:

```
The code execution cannot proceed because glfw3.dll was not found.
```

Place `glfw3.dll` in the same directory as your executable. This is a typical runtime error caused by missing dynamic dependencies.

---

### 📌 Header File Definitions (GLFW Example)

Header files often use macros to handle both static and dynamic linking:

```cpp
#define GLFW_API __declspec(dllimport) // if using DLL
#define GLFW_API                      // if static linking
```

Setting preprocessor definitions like `GLFW_DLL` informs the compiler that you're using the dynamic version.

➡️ **Visual Studio > C/C++ > Preprocessor > Preprocessor Definitions**

```
GLFW_DLL
```

---

### 🔄 Runtime Dynamic Loading (Advanced)

You can also load DLLs entirely at runtime using platform-specific APIs (like `LoadLibrary` on Windows). This gives you full control over which libraries to load and when, even allowing runtime decisions.

---

### ❓ Challenge

Why does the code still work without defining `GLFW_DLL`, even when using the dynamic library? Try to investigate and leave your thoughts in the comments.

---

### ✅ Summary

* Dynamic linking happens at runtime, allowing more flexibility but needing runtime setup.
* Use `glfw3dll.lib` and `glfw3.dll` when linking dynamically.
* Be sure DLLs are in the correct folder or set up runtime paths.

---

🎯 **Tip:** Even if you're using dynamic linking, it's crucial to understand static linking since both are common in C++ development.

📦 Next: We’ll explore runtime dynamic loading for plugins and modularity.
