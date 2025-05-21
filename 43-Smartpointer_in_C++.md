# Smart Pointers in C++

Smart pointers are wrappers around raw pointers that automatically manage memory, helping to prevent memory leaks and dangling pointers. In C++, smart pointers allow you to allocate memory using `new` without needing to explicitly call `delete`. They handle memory deallocation automatically when no longer needed.

---

## 🧵 What Are Smart Pointers?

* Smart pointers automate memory management.
* They wrap raw pointers and handle the `delete` for you.
* You rarely need to call `new` or `delete` directly when using them.

> Many modern C++ developers avoid `new` and `delete` altogether by using smart pointers.

---

## 🧮 Unique Pointer (`std::unique_ptr`)

### Characteristics:

* Owns the memory it points to.
* Cannot be copied (only moved).
* Memory is released when the pointer goes out of scope.

### Syntax:

```cpp
#include <memory>

std::unique_ptr<Entity> entity = std::make_unique<Entity>();
```

Alternatively:

```cpp
std::unique_ptr<Entity> entity(new Entity());  // Not recommended
```

> Use `std::make_unique` for exception safety and readability.

### Why Unique?

* Prevents accidental sharing and double-deletes.
* Copy constructor and assignment are deleted.

### Lifetime:

* When the unique pointer goes out of scope, the destructor runs and memory is freed.

---

## 🧰 Shared Pointer (`std::shared_ptr`)

### Characteristics:

* Reference-counted smart pointer.
* Memory is released only when the last shared pointer referencing the object is destroyed.

### Syntax:

```cpp
#include <memory>

std::shared_ptr<Entity> entity = std::make_shared<Entity>();
```

Or:

```cpp
std::shared_ptr<Entity> entity(new Entity());  // Less efficient
```

### Reference Counting:

* Internally maintains a control block that tracks the number of `shared_ptr`s pointing to the object.
* When reference count drops to zero, memory is freed.

### Example:

```cpp
{
    std::shared_ptr<Entity> a = std::make_shared<Entity>();
    std::shared_ptr<Entity> b = a;  // ref count = 2
}  // ref count = 1 after scope, memory not yet freed
// when b goes out of scope, ref count = 0, memory freed
```

> Use shared pointers when multiple parts of your program share ownership of the object.

---

## 🏠 Weak Pointer (`std::weak_ptr`)

### Characteristics:

* Does not increase reference count.
* Used to observe an object managed by a `shared_ptr` without affecting its lifetime.

### Syntax:

```cpp
std::weak_ptr<Entity> weakEntity = sharedEntity;
```

### Why Use It?

* Prevents circular references (e.g., in graphs, trees).
* Check if object is still alive:

```cpp
if (!weakEntity.expired()) {
    std::shared_ptr<Entity> e = weakEntity.lock();
    // Use e safely
}
```

---

## 🚧 When to Use What

| Type         | Use When                                                 |
| ------------ | -------------------------------------------------------- |
| `unique_ptr` | Default. You only need one owner.                        |
| `shared_ptr` | Multiple owners need to share access to the same object. |
| `weak_ptr`   | You want a non-owning reference to a `shared_ptr`.       |

> Start with `unique_ptr`, then use `shared_ptr` if needed.

---

## ⚠️ Important Notes

* `std::make_unique` and `std::make_shared` are preferred over `new`.
* Smart pointers provide automatic destruction when going out of scope.
* `shared_ptr` adds memory overhead (reference counting).
* Smart pointers are not a complete replacement for `new/delete` but help in most cases.

---

## 🔄 Summary

* Smart pointers simplify memory management.
* They reduce memory leaks and make code safer.
* Use smart pointers to avoid explicit `new`/`delete`.
* Know when and how to use each type effectively.

---

## 📚 Coming Soon

* How smart pointers are implemented.
* Building your own smart pointer (e.g., reference counting).
* In-depth memory management and performance tips.
* How to avoid circular references using `weak_ptr`.

Stay tuned for more advanced topics!

🎥 Watch the full video for live demos and deeper insights.

💬 Join the conversation on Discord or support the series on Patreon!
