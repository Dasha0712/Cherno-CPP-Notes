# C++ Examples Based on The Cherno Videos

This document contains example C++ code with explanations to make it easier to understand. Let's break down each section:

---
## **Example 1: Class Accessibility and Pass-by-Reference**

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl;

class player {
    int x;
    int y;
};

void position(player& player, int xa, int ya) {
    xa = player.x + xa;  
    ya = player.y + ya;
    print(player.x);
    print(player.y);
}

int main() {
    player player;
    position(player, 1, 2);
}
```
### **Explanation:**
- The `player` class has two private member variables `x` and `y`.
- The `position()` function tries to access these variables, but since they are private, it causes a compilation error.

**Fix:** You need to make the `player` class members public:
```cpp
class player {
public:
    int x;
    int y;
};
```
By adding `public:`, the data becomes accessible outside the class.

### **Important Note:**
In line 11, the class members are private by default. Always specify access modifiers (`public`, `private`, or `protected`) to control data accessibility.

---
## **Example 2: Class Method and Initializing Variables**

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl;

class player {
public:
    int x;
    int y = 0;

    void position(int xa, int ya) {
        xa = x + xa;
        ya = y + ya;
        print(xa);
        print(ya);
    }
};

int main() {
    player player;
    player.x = 1;
    player.position(1, 2);
}
```
### **Explanation:**
- In this version, `x` and `y` are public members, making them accessible outside the class.
- The `position()` function is now a **method** within the class.
- `y` is explicitly initialized to `0`.

### **Key Takeaway:**
- Functions defined inside a class are called **methods**.
- Always initialize variables like `y` to avoid undefined behavior.

---
## **Difference Between Pass-by-Value and Pass-by-Reference**

### 1. **Pass-by-Value:**
```cpp
void position(player player, int xa, int ya) {
    xa = player.x + xa;
    ya = player.y + ya;
    print(player.x);
    print(player.y);
}
```
- A copy of the `player` object is passed to the function.
- Changes made inside the function do not affect the original `player` object.

### 2. **Pass-by-Reference:**
```cpp
void position(player& player, int xa, int ya) {
    xa = player.x + xa;
    ya = player.y + ya;
    print(player.x);
    print(player.y);
}
```
- The `player` object is passed by reference, using `&`.
- Any changes made inside the function affect the original `player` object.

### **Key Points:**
- Use pass-by-reference when you want functions to modify the original object.
- Pass-by-reference is also more efficient for large objects, as it avoids making copies.

By understanding these concepts, you'll gain better control over your C++ programs and memory management.

