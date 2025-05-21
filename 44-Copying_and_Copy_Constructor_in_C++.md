# 📋 Copying and Copy Constructors in C++

In C++, copying refers to making a **new object with the same values** as an existing one. Understanding how copying works is critical for performance and correctness. This includes knowing when a copy happens, how to define your own copy behavior, and how to avoid unnecessary copies.

---

## 🔁 What is Copying?

Copying happens when you assign or pass values:

```cpp
int a = 2;
int b = a;  // copy: a and b are now separate
```

Modifying `b` does not affect `a`, because they’re different values in memory.

This also applies to user-defined types:

```cpp
struct Vector2 { float x, y; };

Vector2 a = {2, 3};
Vector2 b = a;  // copy struct
b.x = 5;  // `a.x` remains 2
```

---

## 🎯 Copying Pointers

Pointers themselves are copied like any other value:

```cpp
Vector2* a = new Vector2();
Vector2* b = a;  // same address in memory
```

Now `a` and `b` **point to the same memory**, so changes through one affect the other. You're copying the memory address, **not** the contents.

---

## 📦 Writing a Basic `String` Class

To explore copying further, Cherno builds a basic `String` class:

```cpp
class String {
private:
    char* m_Buffer;
    unsigned int m_Size;

public:
    String(const char* string) {
        m_Size = strlen(string);
        m_Buffer = new char[m_Size + 1];
        memcpy(m_Buffer, string, m_Size);
        m_Buffer[m_Size] = 0;  // null terminator
    }

    ~String() {
        delete[] m_Buffer;
    }

    friend std::ostream& operator<<(std::ostream& stream, const String& string);

    char& operator[](unsigned int index) {
        return m_Buffer[index];
    }
};
```

### Printing the String

```cpp
std::ostream& operator<<(std::ostream& stream, const String& string) {
    stream << string.m_Buffer;
    return stream;
}
```

---

## 💥 Copy Crash Example

```cpp
String string = "Cherno";
String second = string;  // 💣 shallow copy
```

This causes a crash! Why?

* Default copy constructor does a **shallow copy**, meaning `second.m_Buffer == string.m_Buffer`.
* When both are destroyed, the same memory is deleted twice = **crash**.

### Proof:

Both objects point to the **same memory address**:

```cpp
std::cout << string;
std::cout << second;
```

Modifying `second[2] = 'a'` affects `string`.

---

## ✅ Fix: Deep Copy with Copy Constructor

Define your own copy constructor to do a deep copy:

```cpp
String(const String& other) {
    m_Size = other.m_Size;
    m_Buffer = new char[m_Size + 1];
    memcpy(m_Buffer, other.m_Buffer, m_Size + 1);
}
```

Now `string` and `second` have separate memory.

---

## 🧹 Deleting the Copy Constructor

If you don’t want your object to be copyable:

```cpp
String(const String& other) = delete;
```

This is what `std::unique_ptr` does.

---

## 🛑 Avoid Unnecessary Copies

### Bad:

```cpp
void PrintString(String string);
PrintString(myString);  // copies object
```

### Good:

```cpp
void PrintString(const String& string);
```

Always **pass by const reference** to avoid unnecessary copies:

* Faster
* Avoids extra allocations
* Enables temporary values to be passed in

---

## 📌 Summary

| Concept                  | Details                                    |
| ------------------------ | ------------------------------------------ |
| Copying                  | Creates a new object with the same data    |
| Shallow Copy             | Only copies member values (e.g., pointers) |
| Deep Copy                | Allocates new memory and copies data over  |
| Copy Constructor         | Custom constructor to define deep copy     |
| Deleted Copy Constructor | Prevent copying                            |
| Pass by Const Reference  | Avoid unnecessary copies                   |

---

## 🚀 Best Practices

* Always pass objects **by const reference** unless you need a copy.
* Use deep copy when your class **owns memory** (e.g., pointer to a buffer).
* Avoid copying unless you have to — it impacts performance.
* Be aware that default copy constructors may **not** be what you want.

---

## 🧠 Final Thoughts

This video marked the **first deep dive into real C++ coding**, and set the stage for future episodes. Now that you know how copying works, you’ll understand memory ownership and object behavior much better.

👍 Like the video if it helped, and check out [Cherno's Patreon](https://patreon.com/TheCherno) to support future episodes and get early access!
