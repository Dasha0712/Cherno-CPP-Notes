# Object Lifetime in C++

Understanding object lifetime in C++ is crucial for writing reliable and efficient code. This video by The Cherno gives a foundational look at how **stack-based objects** live and die, and how that can be leveraged in real applications.

---

## 🧠 What Is Object Lifetime?

Object lifetime refers to **how long an object exists in memory** before it is destroyed. This depends on where the object is allocated:

* **Stack**: Automatic memory, scoped-based lifetime.
* **Heap**: Manual memory, exists until explicitly deleted.

Cherno focuses here on **stack-based lifetimes**.

---

## 📚 Understanding the Stack

The **stack** is a data structure where variables are "stacked" on top of each other.

Think of it like a stack of books:

* When you enter a **scope**, a book is added.
* Variables inside that scope are stored inside the book.
* When the scope ends, the book is removed—**and so are the variables**.

### Examples of scopes:

```cpp
void MyFunction() { } // function scope
if (x > 0) { }         // if statement scope
for (...) { }          // loop scope
{ int x = 5; }         // anonymous/empty scope
```

Even **class members** follow this rule:

```cpp
class Entity {
    std::string name; // destroyed when the class goes out of scope
};
```

---

## 🧪 Demo: Constructor & Destructor

```cpp
class Entity {
public:
    Entity() { std::cout << "Created Entity\n"; }
    ~Entity() { std::cout << "Destroyed Entity\n"; }
};

void Test() {
    Entity e;  // Stack allocation
}  // Destructor called here
```

### Heap version:

```cpp
Entity* e = new Entity();
// Destructor not called automatically!
```

You must call:

```cpp
delete e;
```

If you don’t, you get a **memory leak**.

---

## 🚫 A Classic Mistake

Don’t return stack memory from a function:

```cpp
int* CreateArray() {
    int arr[50];
    return arr;  // ❌ INVALID: arr is destroyed after return
}
```

### Correct ways:

* **Heap allocation:**

```cpp
int* CreateArray() {
    return new int[50];
}
```

* **Caller provides memory:**

```cpp
void FillArray(int* arr) {
    for (...) arr[i] = ...;
}
```

---

## ✅ Using Lifetime to Your Advantage

Automatic stack destruction can be **extremely useful**.

### Example: Smart Pointer

```cpp
class ScopedPointer {
    Entity* m_Ptr;
public:
    ScopedPointer(Entity* ptr) : m_Ptr(ptr) {}
    ~ScopedPointer() { delete m_Ptr; }
};

{
    ScopedPointer e(new Entity());
} // Automatically deleted
```

This mimics `std::unique_ptr`—a smart pointer.

### Other Use Cases:

* **Timer class**
* **Scoped locks / mutexes**

These automate things like timing, memory release, thread safety.

---

## 🔁 Summary

* Stack objects are automatically destroyed when they go out of scope.
* Returning pointers to stack memory is **dangerous** and leads to **undefined behavior**.
* This destruction can be leveraged to **automate** cleanup (smart pointers, timers, etc).
* You can even build your own wrappers to ensure cleanup.

---

## 🔜 Coming Soon

* Deep dive into the **stack vs heap**
* Smart pointers (`std::unique_ptr`, `std::shared_ptr`, etc)
* More advanced memory management strategies

🎥 Stay tuned and watch Cherno’s full series for hands-on examples.

💬 Join the Patreon/Discord community to help shape the future lessons and get early access!
