# Functions in C++

Functions are blocks of reusable code that perform a specific task. They improve modularity and help manage complexity in large programs.

---

## 🔹 What is a Function?

A function is a named block of code that performs a specific task. It can take inputs (parameters), process them, and optionally return a result.

---

## 🧱 Basic Structure

```cpp
return_type function_name(parameter_list) {
    // function body
}
```

Example:

```cpp
int add(int a, int b) {
    return a + b;
}
```

---

## 📥 Parameters vs Arguments

* **Parameter**: A variable in the function definition.
* **Argument**: The actual value passed to the function when it's called.

Example:

```cpp
void greet(string name) { // 'name' is a parameter
    cout << "Hello, " << name << endl;
}

int main() {
    greet("Alice"); // "Alice" is an argument
}
```

---

## 📤 Types of Function Calls

### 1️⃣ Pass by Value

* A copy of the argument is passed.
* Changes inside the function do not affect the original variable.

```cpp
void update(int x) {
    x = 10;
}

int main() {
    int a = 5;
    update(a);
    cout << a; // Output: 5
}
```

### 2️⃣ Pass by Reference

* The actual variable is passed using a reference (`&`).
* Changes inside the function affect the original variable.

```cpp
void update(int& x) {
    x = 10;
}

int main() {
    int a = 5;
    update(a);
    cout << a; // Output: 10
}
```

### 3️⃣ Pass by Pointer

* Address of the variable is passed.
* Allows modifying the original variable using dereferencing.

```cpp
void update(int* x) {
    *x = 10;
}

int main() {
    int a = 5;
    update(&a);
    cout << a; // Output: 10
}
```

---

## 🧬 Function Overloading

Multiple functions can have the same name with different parameter types or counts.

```cpp
int add(int a, int b) {
    return a + b;
}
float add(float a, float b) {
    return a + b;
}
```

---

## ⚙️ Default Arguments

Function parameters can have default values.

```cpp
void greet(string name = "User") {
    cout << "Hello, " << name << endl;
}
```

---

## 🧮 Inline Functions

Suggests the compiler to insert the function code at the call site.

```cpp
inline int square(int x) {
    return x * x;
}
```

---

## 🔄 Recursive Functions

A function that calls itself.

```cpp
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

---

## 🧪 Lambda (Anonymous) Functions

Introduced in C++11, used for short, unnamed functions.

```cpp
auto square = [](int x) { return x * x; };
cout << square(5); // Output: 25
```

---

## 🧾 Summary Table

| Concept               | Description                               | Example                                         |
| --------------------- | ----------------------------------------- | ----------------------------------------------- |
| Parameter vs Argument | Parameter in definition, argument in call | `greet(string name)` vs `greet("Bob")`          |
| Pass by Value         | Copies data                               | `void func(int x)`                              |
| Pass by Reference     | Uses reference to modify original         | `void func(int& x)`                             |
| Pass by Pointer       | Uses pointer to modify original           | `void func(int* x)`                             |
| Default Arguments     | Provides default values                   | `void greet(string name = "User")`              |
| Inline Function       | Suggests inline expansion                 | `inline int square(int x)`                      |
| Overloading           | Same function name, different params      | `int add(int, int)` / `float add(float, float)` |

---

Let me know if you'd like to expand this with diagrams, flowcharts, or memory illustrations!
