# Cherno C++ Notes

## What the Compiler Does

The compiler converts a text file into an intermediary object file, which is then passed to the linker. We will discuss the linker in the next video.

### Compilation Process

* The compiler goes through several stages before generating the object file:

  1. **Preprocessing:** Handles all preprocessor statements (e.g., `#include`, `#define`, `#if`, `ifdef`).
  2. **Tokenizing and Parsing:** Sorts out the C++ (human-readable) code into a format the compiler can understand, creating an **Abstract Syntax Tree (AST)** — a structured representation of the code.
  3. **Code Generation:** Generates the final machine code from the AST and stores constant data.

## Detailed Compilation Stages

* Once the compiler creates the AST, it begins generating actual machine code.
* It also stores constant data, such as variables.

## Creating Example Files

1. Create two `.cpp` files:

### helloworld.cpp

```cpp
#include <iostream>
void Log(const char* message);
int main() {
    Log("helloworld");
    std::cin.get();
}
```

### Log.cpp

```cpp
#include <iostream>
void Log(const char* message) {
    std::cout << message << std::endl;
}
```

### Compiling the Files

* Compile both `.cpp` files. This will create separate object files (`.obj`).
* These `.cpp` files are called **translation units**.

### Understanding Translation Units

* C++ does not recognize files inherently; they are just a way to provide source code to the compiler.
* Unlike Java, where class names must match file names, C++ files are independent.
* File extensions like `.cpp`, `.c`, and `.h` are conventions. You can use custom extensions if properly configured.

## Creating a New Translation Unit

1. Create another file `math.cpp`:

```cpp
int multiply(int a, int b) {
    return a * b;
}
```

### Object File Sizes

* Build the project and open it in File Explorer.
* Observe that `main.obj` may be larger than `math.obj` because it includes `<iostream>`.

## Preprocessing Stage

* The preprocessor handles directives like `#include`, `#define`, and `#if`.

### Viewing Preprocessed Code

* Go to **Project Properties -> C/C++ -> Preprocessor -> Preprocess to a File**.
* Set **"Preprocess to a File"** to **"Yes"**.
* This generates a `.i` file containing preprocessed code.

### Disabling Preprocessor to File (Important)

* After viewing the preprocessed code, disable **"Preprocess to a File"** when it is not needed.
* If it is enabled, it will not generate an object file.

### Example: Using #include

* Create a header file `endbrace.h` with:

```cpp
}
```

* In `math.cpp`, replace the closing curly brace with:

```cpp
#include "endbrace.h"
```

### Using #define

```cpp
#define INTEGER int
INTEGER multiply(int a, int b) {
    INTEGER result = a * b;
    return result;
}
```

* The preprocessor replaces all `INTEGER` with `int`.

### Conditional Compilation with #if

```cpp
#if 1
int multiply(int a, int b) {
    return a * b;
}
#endif
```

* Setting `#if 1` includes the code.
* Setting `#if 0` excludes the code.

## Understanding Object Files

* Object files are binary and unreadable in a text editor.
* To view human-readable assembly:

  * Go to **Project Properties -> Output Files -> Assembler Output**.
  * Set **"Assembler Output"** to **"Assembly Only Listing"**.

## Code Optimization

* To optimize for speed:

  * Go to **Project Properties -> Optimization -> Optimization**.
  * Set **"Optimization"** to **"Maximum Speed"**.
  * Go to **Project Properties -> Code Generation -> Basic Runtime Checks**.
  * Set **"Basic Runtime Checks"** to **"Default"**.

## Complete Settings Guide

* **Preprocessed Output:** View raw preprocessed code for debugging.
* **Disable Preprocessor to File:** Make sure this is disabled when not needed to get object files.
* **Assembly Output:** View human-readable assembly instructions.
* **Optimization Settings:** Choose the best performance option for your code.