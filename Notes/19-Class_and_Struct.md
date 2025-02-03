# C++ Examples: Classes and Structs

This document explains the difference between `class` and `struct` in C++ and provides examples for better understanding.

---
## **Class**

```cpp
// By default, members of a class are private.
class ExampleClass {
    int x;  // Private by default
};
```
### **Key Point:**
- In classes, member variables are private by default.
- You need to explicitly declare members as public to access them from outside the class.

---
## **Struct**

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl;

struct Person {
    int age;
    int height;
    int weight;
};

int main() {
    Person person;
    person.age = 20;
    person.height = 180;
    person.weight = 70;
    print(person.age);
    print(person.height);
    print(person.weight);
    return 0;
}
```
### **Explanation:**
- In a `struct`, members are public by default.
- Structs are typically used for grouping data.

### **Key Note:**
- Avoid using `struct` for higher complexity concepts like inheritance.
- Use `struct` primarily for simple data structures, such as grouping related variables.

By understanding these concepts, you can effectively decide whether to use `class` or `struct` based on your program requirements.

