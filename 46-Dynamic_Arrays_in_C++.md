# 📦 Dynamic Arrays in C++ (Using `std::vector`)

In C++, a dynamic array is an array that can change size at runtime. The most common way to implement this is by using the `std::vector` class from the Standard Template Library (STL).

---

## 📚 What is the Standard Template Library (STL)?

* STL is a collection of **container types** (like arrays, lists, maps) that store data.
* It's templated: you can choose **any type** to store inside the container.
* You don’t need to understand templates to use STL containers.

---

## 📌 Introducing `std::vector`

* `std::vector` is a dynamic array.
* Unlike built-in arrays, vectors can grow or shrink in size.
* Vectors are stored in **contiguous memory**, so iteration is cache-friendly and fast.

### ⚠️ Misleading Name

* Despite the name, `std::vector` is **not** a mathematical vector.
* It's more like an `ArrayList` or `dynamic array`.

---

## 🛠 How `std::vector` Works Internally

* Initially allocates memory for a certain number of elements.
* When more elements are added than it can hold, it:

  1. Allocates a larger memory block.
  2. Copies existing data.
  3. Deletes the old block.
* This **copying** can be expensive if not handled properly.

---

## 🧪 Creating a Dynamic Array

### Define a Custom Struct

```cpp
struct Vertex {
    float x, y, z;
};

std::ostream& operator<<(std::ostream& stream, const Vertex& v) {
    stream << v.x << ", " << v.y << ", " << v.z;
    return stream;
}
```

### Create a Vector of Vertices

```cpp
#include <vector>

std::vector<Vertex> vertices;
vertices.push_back({1, 2, 3});
vertices.push_back({4, 5, 6});
```

---

## 🔁 Iterating Through a Vector

### Classic For Loop

```cpp
for (size_t i = 0; i < vertices.size(); i++) {
    std::cout << vertices[i] << std::endl;
}
```

### Range-Based For Loop

```cpp
for (const Vertex& v : vertices) {
    std::cout << v << std::endl;
}
```

**Tip:** Always use `const &` to avoid copying objects.

---

## 🧹 Managing Vector Memory

### Clear All Elements

```cpp
vertices.clear();
```

### Remove a Specific Element

```cpp
// Removes second element (index 1)
vertices.erase(vertices.begin() + 1);
```

---

## 🧠 Memory and Performance Tips

* Prefer storing **objects directly** (not pointers) for better performance.
* Storing objects inline ensures contiguous memory layout = cache-friendly.
* Only store pointers if:

  * You need polymorphism (inheritance)
  * You require shared ownership or manual memory control

### Function Parameter Tips

Always pass vectors by reference to avoid copying:

```cpp
void PrintVertices(const std::vector<Vertex>& vertices);
```

---

## 📈 Why Not Preallocate a Huge Array?

* Wastes memory if only a few elements are used.
* Instead, let `std::vector` grow as needed, or use `reserve()` to optimize:

```cpp
vertices.reserve(1000);  // Preallocate space for 1000 vertices
```

---

## 🧪 Summary

| Feature                     | `std::vector` |
| --------------------------- | ------------- |
| Dynamic size                | ✅             |
| Contiguous memory           | ✅             |
| Random access               | ✅             |
| Automatic memory management | ✅             |
| Easy to use                 | ✅             |

---

## 🚀 What’s Next?

This was a beginner-friendly intro to `std::vector`. In the **next episode**, Cherno dives into:

* Reallocation optimization
* Avoiding unnecessary copies
* Advanced usage patterns

---

## 💡 Final Thoughts

Vectors are one of the most essential tools in modern C++. They're flexible, powerful, and easy to use — as long as you understand how to avoid performance pitfalls.

👍 Like the video if it helped, and check out [Cherno's Patreon](https://patreon.com/TheCherno) to support the series and get early access!
