# Local Static in C++

In this lesson, we explore another usage of the `static` keyword in C++—**local static variables**.

---

## 🔁 Lifetime vs Scope

When declaring variables in C++, it's crucial to understand two concepts:

* **Lifetime**: How long a variable remains in memory before being destroyed.
* **Scope**: Where in the code the variable can be accessed.

Example:

```cpp
void Function() {
    int x = 0; // Lifetime: during each function call, Scope: only within Function
}
```

---

## 🔒 Static in Local Scope

A **local static variable**:

* Has a **lifetime of the entire program** (like a global variable).
* Has **scope limited to where it's declared** (like a local variable).

This is very different from global or class-level `static` variables, even though they share the lifetime characteristic.

### Function Example:

```cpp
void Function() {
    static int i = 0;
    std::cout << ++i << std::endl;
}

int main() {
    for (int j = 0; j < 5; ++j) Function();
    return 0;
}
```

**Output:**

```
1
2
3
4
5
```

* On the **first call**, `i` is initialized.
* On **subsequent calls**, the same variable is reused.

Contrast with a non-static version, where `i` is reinitialized to `0` every time, so output would always be `1`.

---

## 🚫 Why Not Use a Global Variable?

```cpp
static int i = 0; // global static
```

* Exposes `i` outside of the function, leading to potential misuse.

```cpp
void Function() {
    static int i = 0; // local static - safer
    std::cout << ++i << std::endl;
}
```

Local static helps **encapsulate state** within the function.

---

## 🧱 Singleton Example

Goal: Only one instance of a class exists (Singleton pattern).

### Old Way (More Verbose):

```cpp
class Singleton {
public:
    static Singleton& Get() {
        return *s_Instance;
    }

    void Hello() {}

private:
    static Singleton* s_Instance;
};

Singleton* Singleton::s_Instance = new Singleton();
```

### Cleaner Way Using Local Static:

```cpp
class Singleton {
public:
    static Singleton& Get() {
        static Singleton instance;
        return instance;
    }

    void Hello() {}
};
```

* **`static Singleton instance;`** ensures one-time initialization.
* Lifetime: entire program.
* Scope: within the `Get()` function.

This simplifies your code **greatly** and **encapsulates** the instance properly.

> ⚠️ Without `static`, the object would be destroyed at the end of the function call, making it unsafe to return by reference.

---

## 💬 When to Use

* Replace global variables you want to hide.
* Lazy initialization of objects.
* Singleton patterns.
* Retain state across function calls.

While some discourage this practice due to testability or hidden state issues, **it is safe and valid**, and often makes your code **cleaner and more concise**.

---

## ✅ Summary

* Local static variables have program-wide lifetime, but limited scope.
* Great for retaining state in a function without polluting global space.
* Perfect for Singleton patterns and lazy initialization.
* Use it wisely to keep code clean and maintainable.
