## Optimizing the Usage of `std::vector` in C++

In this video, Cherno introduces **optimization techniques** using `std::vector` in C++. It's the first video in the series focused on **performance tuning**.

---

### 🔥 Why Optimization?

* **C++ is built for performance.** It's often chosen for scenarios where **low-level optimizations** are needed.
* One of the **most important principles** in optimization: **Know your environment**.

  * Understand: How does it work? What happens behind the scenes? How can we avoid inefficiencies?

### 🧠 Focus: `std::vector`

* Goal: Understand **how vector works internally**, and how we can optimize its usage.
* Specifically, we want to reduce **copies** of our objects when working with vectors.

---

### ⚙️ How `std::vector` Works

* When you `push_back()` into a vector:

  * If there’s **enough capacity**, the element is added.
  * If there’s **not enough capacity**, the vector:

    1. **Allocates new memory**.
    2. **Copies all old elements** into the new memory.
    3. **Deletes old memory**.

🔁 This **reallocation and copying** can be **very expensive**.

---

### 🧪 Example: Vertex Class

```cpp
struct Vertex {
    float x, y;

    Vertex(float x, float y) : x(x), y(y) {}

    Vertex(const Vertex& other)
        : x(other.x), y(other.y) {
        std::cout << "Copied!\n";
    }
};
```

* The `copy constructor` logs when a copy occurs.
* Add elements to vector:

```cpp
std::vector<Vertex> vertices;

vertices.push_back(Vertex(1, 2));
vertices.push_back(Vertex(3, 4));
vertices.push_back(Vertex(5, 6));
```

### ❗ Result: 6 Copies

* Each time you `push_back`, the element is first **constructed on the stack** in `main()`.
* Then it's **copied** into the vector’s internal memory.
* Additionally, **vector resizes itself** when out of capacity, causing **even more copies**.

---

### 🧠 Optimization Strategy #1: Use `reserve()`

Instead of letting the vector resize multiple times, **pre-allocate enough memory**.

```cpp
std::vector<Vertex> vertices;
vertices.reserve(3); // Reserve space for 3 elements
```

✅ Now the vector won’t reallocate when adding 3 elements → **fewer copies**

### ❗Important:

* Don’t confuse `reserve()` with `resize()` or passing size to constructor.

  * `reserve(3)` → Allocates memory, doesn’t create any objects.
  * `resize(3)` or `std::vector<Vertex> vertices(3)` → Actually constructs 3 default-initialized `Vertex` objects (needs default constructor).

---

### 🧠 Optimization Strategy #2: Use `emplace_back()`

Avoid the copy **completely** by constructing the object **directly inside the vector’s memory**.

```cpp
vertices.emplace_back(1, 2);
vertices.emplace_back(3, 4);
vertices.emplace_back(5, 6);
```

✅ Now there are **zero copies**.

* `emplace_back()` takes constructor parameters and constructs the object **in place**.
* Much more efficient than creating it first and copying.

---

### ✅ Final Optimized Code

```cpp
std::vector<Vertex> vertices;
vertices.reserve(3);

vertices.emplace_back(1, 2);
vertices.emplace_back(3, 4);
vertices.emplace_back(5, 6);
```

### ✅ Output

```
(no copy messages)
```

Zero copies. Much faster. More efficient.

---

### 💡 Takeaways

* **Understand your tools**: Know how `std::vector` behaves internally.
* **Avoid unnecessary copies**:

  * Use `reserve()` to prevent reallocations.
  * Use `emplace_back()` to construct in-place.
* These two small changes result in **much better performance**, especially at scale.

---

> Cherno: "This isn't even hard to write. It's just about knowing what's going on."

This is just the beginning of performance optimization in C++. The rest of the series will dive even deeper.

Support Cherno on [Patreon](https://patreon.com/thecherno) for early access and more content!

---

Next up: More on object lifetimes, copying, move semantics, and performance!
