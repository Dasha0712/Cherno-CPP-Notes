# How C++ Works

When writing a C/C++ program, the source code must go through several stages before it becomes an executable file. Below is a detailed explanation of how this process works, including key concepts and best practices.

## Compilation Process Overview
The process of converting a source file into a binary file involves the following steps:

1. **Preprocessing**
2. **Compilation**
3. **Assembly**
4. **Linking**

### 1. Preprocessing
Preprocessor statements begin with a `#` symbol and are handled before actual compilation starts.

```c
#include <stdio.h>
```

- The `#include <stdio.h>` statement copies all the contents of the `stdio.h` file and pastes it into the current file.
- The first thing a compiler does when receiving a source file is **preprocessing**, where it processes all preprocessor directives.

### 2. Compilation
The compiler translates the preprocessed source code into assembly language, producing an **object file** with a `.obj` or `.o` extension.

### 3. Assembly
The assembler converts the assembly language file into machine code, creating an object file.

### 4. Linking
The **linker** combines multiple object files into a single executable file.

- Each C++ source file (`.cpp`) gets compiled into an object file (`.obj` or `.o`).
- The linker stitches these separate object files together into a final binary executable (`.exe`).
- If any referenced function is missing, a **linker error** occurs.

## Debug Mode vs. Release Mode (Visual Studio)

- **Debug Mode**: Slower execution due to debugging symbols and no optimizations.
- **Release Mode**: Faster execution because optimizations are turned on.

## Understanding Compilation in Visual Studio

### 1. Compiling a Single File (Without Linking)
- Use `Ctrl + F7` to compile a single file.
- This generates an **object file** without linking.

### 2. Customizing Shortcut Keys
If you want to change shortcut keys for compiling:

```
Right-click (Top Bar) -> Build -> Auto Remove Buttons -> Customize -> Add Command -> Build -> Compile -> Assign Shortcut
```

### 3. Finding Compiled Files
After compiling a file:
- Navigate to `Project Folder -> Debug Folder` to find `main.obj`.
- After building the project, the `Debug Folder` will contain the `project_name.exe` executable file.

## Multiple File Compilation Example
### `main.cpp`
```cpp
#include <iostream>
void log(); // Declaration

int main() {
    log(); // Call log function
    return 0;
}
```

### `log.cpp`
```cpp
#include <iostream>
void log() { // Definition
    std::cout << "Hello, World!" << std::endl;
}
```

### Why Declaration is Needed
If you remove the declaration (`void log();`) from `main.cpp`, you will get a **compilation error** because `main.cpp` does not know about the `log()` function.

### Understanding Declaration vs. Definition
- **Declaration**: Tells the compiler that a function exists (but does not define it).
- **Definition**: Provides the actual implementation of the function.

Example:
```cpp
// Declaration
void log();

// Definition
void log() {
    std::cout << "Hello, World!" << std::endl;
}
```

### Role of the Linker
- The compiler does not know where `log()` is defined; it just trusts the declaration.
- The **linker** ensures that the correct function definition is used.
- If the definition is missing, a **linker error** occurs.

### What Happens if Function Names Differ?
If you change `log` to `logg` in `log.cpp`, the linker will not find the function and produce a **linker error**.

---

This guide provides a structured and easy-to-understand explanation of how C++ works. Let me know if you need further clarification! 🚀

