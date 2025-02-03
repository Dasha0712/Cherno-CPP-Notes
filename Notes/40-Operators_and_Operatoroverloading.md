# Operator Overloading in C++

## Introduction
Operator overloading allows us to redefine the behavior of operators for user-defined types. This makes mathematical operations more intuitive and improves code readability.

---

## Example: Overloading `+`, `*`, `==`, and `!=` Operators
```cpp
#include <iostream>

class Vector2 {
private:
    float x, y;
public: 
    Vector2(float x, float y)
        : x(x), y(y) {}
    
    // Addition function
    Vector2 Add(const Vector2& other) const {
        return Vector2(x + other.x, y + other.y);
    }
    
    // Overloading + operator
    Vector2 operator+(const Vector2& other) const {
        return Add(other);
    }
    
    // Multiplication function
    Vector2 Multiply(const Vector2& other) const {
        return Vector2(x * other.x, y * other.y);
    }
    
    // Overloading * operator
    Vector2 operator*(const Vector2& other) const {
        return Multiply(other);
    }
    
    // Overloading == operator
    bool operator==(const Vector2& other) const {
        return x == other.x && y == other.y;
    }
    
    // Overloading != operator
    bool operator!=(const Vector2& other) const {
        return !(*this == other);
    }

    // Print function for debugging
    void Print() const {
        std::cout << "(" << x << ", " << y << ")" << std::endl;
    }
};

int main() {
    Vector2 position(4.0f, 4.0f);
    Vector2 speed(0.5f, 1.5f);
    Vector2 powerup(1.1f, 1.1f);

    // Using functions
    Vector2 result1 = position.Add(speed.Multiply(powerup));
    
    // Using overloaded operators
    Vector2 result2 = position + speed * powerup;
    
    // Displaying results
    std::cout << "Result 1: ";
    result1.Print();
    std::cout << "Result 2: ";
    result2.Print();
    
    // Checking equality
    if (result1 == result2) {
        std::cout << "Both results are equal." << std::endl;
    } else {
        std::cout << "Both results are not equal." << std::endl;
    }
    
    return 0;
}
```

---

## Explanation
- **Addition (`+`)**: Uses the `Add` method to sum two vectors.
- **Multiplication (`*`)**: Uses the `Multiply` method to multiply corresponding components.
- **Equality (`==`)**: Compares if two vectors are the same.
- **Inequality (`!=`)**: Uses `==` to determine inequality.
- **Chained Operations**: The `speed * powerup` calculation happens first, then the result is added to `position`.
- **Function vs Operator Usage**: `position.Add(speed.Multiply(powerup))` does the same as `position + speed * powerup`, but the latter is cleaner.

> **Best Practice:** Overloading operators improves readability but should be used logically and consistently.

---

## Summary
| Operator | Function | Description |
|----------|---------|-------------|
| `+` | `Add()` | Adds two vectors |
| `*` | `Multiply()` | Multiplies two vectors element-wise |
| `==` | `operator==` | Checks if two vectors are equal |
| `!=` | `operator!=` | Checks if two vectors are not equal |

By using operator overloading, we make vector operations more intuitive and maintainable. 🚀

