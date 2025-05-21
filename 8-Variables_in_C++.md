# Variables in C++

Variables in C++ are containers for storing data values. They are essential building blocks of any program, allowing developers to store, manipulate, and retrieve data.

---

## 🧠 What is a Variable?

A variable is a named storage that holds a value which can be changed during program execution. It has:

* A **name** (identifier)
* A **type** (such as `int`, `float`, etc.)
* A **value** (data stored in memory)
* A **memory location** (address)

---

## 🛠️ Declaring Variables

```cpp
int age;
float height = 5.9;
char grade = 'A';
```

---

## 🧬 Data Types

### 🔢 Primitive Types

* `int` – Integer values
* `float` – Floating-point numbers
* `double` – Double precision floating point
* `char` – Single character
* `bool` – Boolean values (`true` or `false`)

### 🧰 Derived Types

* Arrays
* Pointers
* Functions
* References

### 🏗️ User-Defined Types

* `struct`, `union`, `class`, `enum`

---

## 📦 Variable Initialization

```cpp
int x = 10;        // Copy initialization
int y(20);         // Direct initialization
int z{30};         // Uniform initialization (C++11+)
```

---

## 🌍 Scope of Variables

* **Local Variables**: Declared inside a function or block
* **Global Variables**: Declared outside all functions
* **Static Variables**: Retain value between function calls
* **Class/Instance Variables**: Used in OOP inside classes

---

## 📂 Storage Classes

* `auto`: Default for local variables
* `register`: Suggests storing in CPU register
* `static`: Persists across function calls
* `extern`: Declares a global variable defined elsewhere
* `mutable`: Allows modification in `const` objects

---

## 🧮 Constant and Read-only Variables

* `const`: Cannot be modified after initialization

```cpp
const int MAX = 100;
```

* `constexpr`: Evaluated at compile time (C++11+)

```cpp
constexpr int SIZE = 10;
```

---

## 🪪 Variable Qualifiers

* `volatile`: Prevents compiler optimization
* `restrict` (C++23): Optimization hint about pointers

---

## 🧑‍💻 Best Practices

* Always initialize variables
* Use `const` wherever applicable
* Limit scope of variables
* Avoid using global variables
* Prefer `constexpr` for compile-time constants

---

## 🧱 Common Errors

* **Uninitialized variables**: Can cause unpredictable behavior
* **Redeclaration**: Same variable name in the same scope
* **Type mismatch**: Assigning incompatible types
* **Shadowing**: Local variable hides global one

---

## 📝 Naming Conventions in C++

Naming conventions vary slightly among major organizations but adhere to clarity, consistency, and readability.

### 🔹 General Guidelines (Agreed Across Most Style Guides)

* Use descriptive names
* Avoid single-letter variables except for counters
* Use consistent casing (camelCase, snake\_case, PascalCase)
* Avoid starting with underscores or using reserved keywords

### 🔸 NASA C++ Style

* `snake_case` for variables and functions
* `ALL_CAPS` for constants/macros
* Prefix pointers with `p_`, globals with `g_`

### 🔸 Google C++ Style Guide

* `camelCase` for variables and functions
* `PascalCase` for classes
* `kVariableName` for constants
* Namespace names in `lowercase`

### 🔸 Amazon/AWS Style

* `camelCase` for local variables
* `PascalCase` for class/struct
* Constants prefixed with `g_` or `k`
* Comments and documentation are emphasized

### 🔸 Facebook (Meta) Style

* Similar to Google style
* Avoids Hungarian notation
* Encourages long, descriptive names
* `CamelCase` for type names, `camelCase` for variable/methods

---

## 🧾 Summary Table

| Feature              | Example                   | Notes                     |
| -------------------- | ------------------------- | ------------------------- |
| Variable Declaration | `int x = 10;`             | Allocate and assign       |
| Constant             | `const float PI = 3.14;`  | Value can't change        |
| Scope                | `local`, `global`         | Determines visibility     |
| Storage Class        | `static`, `extern`        | Controls lifetime/linkage |
| Naming Convention    | `camelCase`, `snake_case` | Use consistently          |

---

Let me know if you'd like diagrams, memory layout visuals, or interactive examples added!
