# C++ Function Overloading and Templates (Cherno Video Examples)

## 1. Function Overloading Example

```cpp
#include<iostream>

void print(int num) {
    std::cout << num << std::endl;
}

void print(std::string str) {
    std::cout << str << std::endl;
}

void print(float num) {
    std::cout << num << std::endl;
}

int main() {
    print(35);
    print("satorou gojo");
    print(99.78f);
}
```

### Explanation:
- We have three overloaded `print` functions.
- Each function handles a different type: `int`, `string`, and `float`.
- This approach requires writing multiple functions with similar logic, which is inefficient.

---

## 2. Solution Using Templates

```cpp
#include<iostream>

template<typename T>
void print(T num) {
    std::cout << num << std::endl;
}

int main() {
    print<int>(35);
    print<std::string>("satorou gojo");
    print<float>(99.78f);
}
```

### Explanation:
- **Templates** allow us to write a single `print` function that works for any type.
- The function only exists when it is called with a specific type (`T`).
- This makes the code more reusable and concise.

---

## 3. Proving That Templates Do Not Exist Until Called

```cpp
#include<iostream>

template<typename T>
void print(T num) {
    std::cout << num1 << std::endl; // This contains an intentional error
}

int main() {
    // Uncommenting the following line and compiling with Ctrl + F7
    // will not show an error until the function is called.
    // print(456);

    std::cout << "I HAVE NO ENEMIES" << std::endl;
}
```

### Explanation:
- The error (`num1` instead of `num`) will **not** cause a compilation error unless `print()` is actually called.
- This proves that templates only exist when instantiated with a type.

---

## 4. Template Class Example

```cpp
#include<iostream>

template<int N, typename T>
class Array {
private:
    T m_array[N];
public:
    int getSize() const { return N; }
};

int main() {
    Array<5, int> array; // Order is important (size first, then type)
    std::cout << array.getSize() << std::endl;
    std::cout << "I HAVE NO ENEMIES" << std::endl;
}
```

### Explanation:
- **Template classes** allow us to create a flexible array class.
- The `N` parameter defines the size at compile-time.
- The `T` parameter defines the data type.
- This enables us to create type-safe arrays of any size and type.

---

### Summary
✅ Function overloading requires multiple function definitions.
✅ Templates allow us to write a single function for multiple types.
✅ Templates do not exist until instantiated.
✅ Template classes provide flexibility with both size and type.

This Markdown file makes it easy to understand templates and their use cases in C++. 🚀