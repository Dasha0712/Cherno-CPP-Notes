# Understanding Static vs Non-Static Variables in C++

This document explores the difference between static and non-static variables in C++ using examples.

---
## **1. Without Static Keyword: Each Object Has Its Own Copy of Non-Static Variables**

```cpp
#include <iostream>

class Entity {
public:
    int x; // Non-static variable
    int y; // Non-static variable

    void Print() {
        std::cout << "x: " << x << ", y: " << y << std::endl;
    }
};

int main() {
    Entity e1, e2; // Two objects created

    e1.x = 10;
    e1.y = 20;

    e2.x = 30; // This does NOT affect e1.x
    e2.y = 40;

    e1.Print(); // Output: x: 10, y: 20
    e2.Print(); // Output: x: 30, y: 40

    return 0;
}
```
### **Output:**
```
x: 10, y: 20
x: 30, y: 40
```
### **Explanation:**
- Each object (`e1`, `e2`) has its own copy of `x` and `y`.
- Changes to `x` and `y` in one object do not affect the other.

---
## **2. With Static Keyword: All Objects Share the Same Copy of Static Variables**

```cpp
#include <iostream>

class Entity {
public:
    static int x;
    static int y;

    void Print() {
        std::cout << "x: " << x << ", y: " << y << std::endl;
    }
};

int Entity::x;
int Entity::y;

int main() {
    Entity e1, e2; // Two objects created

    e1.x = 10;
    e1.y = 20;

    e2.x = 30; // This DOES affect e1.x
    e2.y = 40;

    e1.Print(); // Output: x: 30, y: 40
    e2.Print(); // Output: x: 30, y: 40

    return 0;
}
```
### **Output:**
```
x: 30, y: 40
x: 30, y: 40
```
### **Explanation:**
- `x` and `y` are declared as static variables.
- Static variables are shared by all objects of the class.
- Changes made to `x` and `y` through one object are reflected in all other objects.

---
### **Key Points:**
1. **Non-Static Variables:**
   - Memory is automatically allocated for each object.
   - Each object has its own copy of non-static variables.

2. **Static Variables:**
   - Memory is allocated in a special memory area called the **data segment** (not on the stack or heap).
   - Static variables are shared by all objects of the class.
   - Memory is NOT automatically allocated per object.

3. **Static Methods:**
   - A class can also have static methods.
   - Static methods can only access static variables; they cannot access non-static variables.

By understanding the difference between static and non-static variables, you can better manage memory and control program behavior in your C++ applications.

