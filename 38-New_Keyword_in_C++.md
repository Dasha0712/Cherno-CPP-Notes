# `new` Keyword in C++

The `new` keyword in C++ is used to dynamically allocate memory on the **heap**. It's crucial to understand this deeply because it involves how memory is managed, which directly affects performance and control in C++ applications.

---

## 🧠 Why `new` Is Important

* If you're writing in C++, you should care about **memory, performance, and optimization**.
* C++ gives you more memory control compared to managed languages like Java or C#.
* In Java or C#, memory is managed (via garbage collection), but in C++, **you must manage it manually**.

> If you don’t care about performance and memory control, you might want to reconsider why you're using C++.

---

## 🧱 What `new` Actually Does

When you use `new`, several steps happen under the hood:

### Example:

```cpp
int* ptr = new int;
```

C++ will:

1. Determine the size of the type (e.g., 4 bytes for `int`).
2. Request that many bytes from the OS/C runtime (typically via `malloc`).
3. Locate a block of memory (e.g., using a **free list** internally).
4. Return a pointer to the allocated block.
5. **Call the constructor** if it’s a class.

### Arrays:

```cpp
int* arr = new int[50];  // 200 bytes for 50 ints
```

* Allocates 200 bytes (50 × 4).
* Finds 200 bytes **contiguously in memory**.

---

## 💡 Allocating Classes

Suppose you have:

```cpp
class Entity {
public:
    std::string name;
};
```

You can allocate:

```cpp
Entity* e = new Entity();
Entity* list = new Entity[50];
```

* `new Entity()` allocates and constructs one entity.
* `new Entity[50]` allocates 50 entities contiguously and calls each constructor.

---

## 🧼 You MUST Free Memory

Memory from `new` stays allocated **until you free it**.

### Single variable:

```cpp
delete ptr;
```

### Array:

```cpp
delete[] arr;
```

> If you allocate with `new[]`, you must use `delete[]`. Using the wrong delete causes undefined behavior.

---

## 🛠️ Internals of `new`

* `new` is an **operator** like `+` or `=`.
* You can overload it:

```cpp
void* operator new(size_t size);
```

* Behind the scenes, `new` typically uses `malloc()` to get memory.
* Example equivalent:

```cpp
Entity* e = (Entity*)malloc(sizeof(Entity));  // Not recommended!
```

* But this **does not call the constructor**.

✅ Use:

```cpp
Entity* e = new Entity();  // Recommended
```

---

## 🔂 `delete` Operator

* `delete` is also an operator.
* Calls the destructor, then `free()`.
* You must use `delete` to release memory manually.

If you forget to `delete`, the memory is never returned to the system = **memory leak**.

---

## 🧠 Special Case: Placement `new`

* Lets you specify where in memory to construct an object:

```cpp
void* buffer = malloc(sizeof(Entity));
Entity* e = new (buffer) Entity();
```

* Used for **custom allocators**, **optimization**, and **manual memory management**.
* `new` does not allocate memory here; it just constructs the object.

---

## 📌 Rule Summary

| Allocation     | Use                       |
| -------------- | ------------------------- |
| `new Type`     | Allocate single object    |
| `new Type[n]`  | Allocate array of objects |
| `delete ptr`   | Free single object        |
| `delete[] ptr` | Free array                |

Always match `new` with `delete`, and `new[]` with `delete[]`.

---

## ⚠️ Caution for Beginners

Avoid this:

```cpp
Entity* e = (Entity*)malloc(sizeof(Entity));
```

Because:

* Constructor is **not called**.
* Error-prone, harder to read, and poor style.

Use `new` instead:

```cpp
Entity* e = new Entity();
```

---

## 🤓 Extra Facts

* `new` calls `operator new`, which can be overloaded.
* Returns a `void*` which is typecast internally.
* `malloc` and `new` are **not the same**—only `new` calls the constructor.
* If you use `new[]`, always use `delete[]`.
* There is a different delete operator for arrays.
* We'll explore **smart pointers**, **scope-based cleanup**, and **reference counting** in future videos.

---

## 📦 Coming Up

* More memory management tips
* How to avoid memory leaks
* Smart pointers (`std::unique_ptr`, `std::shared_ptr`)
* Scope-based resource management

🎥 Watch the full episode and others on my YouTube channel.

💬 Join the discussion on Discord or support me on Patreon to help shape these lessons!
