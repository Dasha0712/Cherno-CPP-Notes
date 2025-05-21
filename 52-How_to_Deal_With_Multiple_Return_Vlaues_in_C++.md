## How to Deal with Multiple Return Values in C++

Hey, what's up guys! My name is The Cherno—welcome back to my C++ series. In this episode, we're going to talk about tuples, pairs, and different ways to return multiple values from a function in C++. I'll also show you how I personally like to handle this.

This topic came up as a spin-off from a recent OpenGL video where we discussed a more convenient way to read shaders. If you're following this C++ series and you're also interested in graphics programming, definitely check out the OpenGL series.

### The Problem

Suppose you have a function that needs to return **two strings**, or maybe an `int` and a `std::string`. C++ functions traditionally return only one value. So how do we return multiple values?

Let’s explore the most common ways:

---

### 1. **Using Output Parameters (References or Pointers)**

This is a classic method. Here’s a simple version:

```cpp
void ParseShader(std::string& vertexSource, std::string& fragmentSource) {
    vertexSource = "vertex shader source";
    fragmentSource = "fragment shader source";
}

int main() {
    std::string vs, fs;
    ParseShader(vs, fs);
    // Use vs and fs
}
```

* **Pros**: No extra return structure, efficient (avoids extra copying).
* **Cons**: Slightly clunky syntax, not very expressive.

You can also use pointers if you want to optionally skip some output:

```cpp
void ParseShader(std::string* vertexSource, std::string* fragmentSource) {
    if (vertexSource) *vertexSource = "vertex";
    if (fragmentSource) *fragmentSource = "fragment";
}
```

---

### 2. **Returning a `std::array` or `std::vector`**

Use this if you want to return multiple items **of the same type**:

```cpp
std::array<std::string, 2> ParseShader() {
    std::array<std::string, 2> result;
    result[0] = "vertex shader";
    result[1] = "fragment shader";
    return result;
}
```

Or using `std::vector`:

```cpp
std::vector<std::string> ParseShader() {
    return { "vertex shader", "fragment shader" };
}
```

* **Use `array`** when the size is fixed.
* **Use `vector`** when you might want a dynamic number of return values.

---

### 3. **Using `std::pair`**

For two values of potentially different types:

```cpp
#include <utility> // for std::pair

std::pair<std::string, std::string> ParseShader() {
    return std::make_pair("vertex shader", "fragment shader");
}

int main() {
    auto shaderSources = ParseShader();
    std::string vs = shaderSources.first;
    std::string fs = shaderSources.second;
}
```

* **Simple and expressive**.
* **Limited to exactly two values**.

---

### 4. **Using `std::tuple`**

For returning more than two values or values of different types:

```cpp
#include <tuple>

std::tuple<std::string, std::string, int> ParseShader() {
    return std::make_tuple("vertex shader", "fragment shader", 42);
}

int main() {
    auto [vs, fs, version] = ParseShader();
}
```

> Requires C++17 or later for structured bindings.

---

### 5. **Creating a Custom Struct (Recommended)**

This is **Cherno's favorite method**, especially when working on real-world projects.

```cpp
struct ShaderProgramSource {
    std::string VertexSource;
    std::string FragmentSource;
};

ShaderProgramSource ParseShader() {
    ShaderProgramSource source;
    source.VertexSource = "vertex shader";
    source.FragmentSource = "fragment shader";
    return source;
}

int main() {
    ShaderProgramSource shader = ParseShader();
    // Use shader.VertexSource and shader.FragmentSource
}
```

* **Highly readable and extendable**.
* **Best for maintainable and scalable codebases**.

---

### Summary

| Method            | Return Type            | Pros                        | Cons                         |
| ----------------- | ---------------------- | --------------------------- | ---------------------------- |
| Output Parameters | `void + refs`          | Efficient                   | Less readable, clunky syntax |
| Array / Vector    | `std::array`, `vector` | Simple for same-type values | Can't handle different types |
| `std::pair`       | `std::pair<T1,T2>`     | Easy for two values         | Limited to two               |
| `std::tuple`      | `std::tuple<Ts...>`    | Flexible                    | Less readable                |
| Custom Struct     | `struct`               | Clean, maintainable         | Slightly more typing         |

If you care about performance and clarity, custom structs are often the best approach. But C++ gives you many tools to pick the right one depending on your use case.

Stay tuned for more advanced topics in C++!
