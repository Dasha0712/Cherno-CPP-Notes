# Mutable Keyword in C++

## What is Mutable?

* The `mutable` keyword in C++ allows modification of a variable even if it is part of a constant object.
* The English word "mutable" means "liable to change" — the opposite of "immutable" (cannot change).
* In C++, `mutable` has two main uses:

  1. Modifying class members in `const` methods.
  2. Modifying captured variables in `lambda` expressions.

## 1. Using Mutable with Class Members

* Normally, if a method is marked as `const`, it cannot modify any member variables of the class.
* This is useful because it guarantees that the method does not alter the object.

### Example without Mutable

```cpp
#include <iostream>
#include <string>

class Entity {
private:
    std::string name;
    int debugCount = 0; // Debug counter

public:
    const std::string& getName() const {
        debugCount++; // Error: Cannot modify member variable in const method
        return name;
    }
};
```

* The code above gives an error because `debugCount` is being modified in a `const` method.

### Solving with Mutable

* To allow modification of `debugCount` in the `const` method, use the `mutable` keyword.

```cpp
#include <iostream>
#include <string>

class Entity {
private:
    std::string name;
    mutable int debugCount = 0; // Mutable variable

public:
    const std::string& getName() const {
        debugCount++; // Allowed because of mutable
        return name;
    }
};
```

* Now, the `debugCount` variable can be modified even in the `const` method because it is marked `mutable`.

## 2. Using Mutable with Lambda Expressions

* The second use of `mutable` is in lambda expressions.
* Normally, captured variables in lambdas are `const` by default when captured by value.

### Example without Mutable

```cpp
#include <iostream>

int main() {
    int x = 8;
    auto lambda = [x]() {
        x++; // Error: Cannot modify captured variable
        std::cout << x << std::endl;
    };

    lambda();
}
```

* This code gives an error because `x` is captured by value, making it constant within the lambda.

### Using Mutable with Lambda

* The `mutable` keyword allows modifying captured variables even if they are captured by value.

```cpp
#include <iostream>

int main() {
    int x = 8;
    auto lambda = [x]() mutable {
        x++; // Now allowed
        std::cout << x << std::endl; // Prints 9
    };

    lambda();
    std::cout << x << std::endl; // Prints 8 (original x unchanged)
}
```

* The `mutable` keyword in this case allows modification of a copy of `x` inside the lambda.
* The original `x` outside the lambda remains unchanged.

## Conclusion

* The `mutable` keyword is most commonly used with `const` class methods, allowing specific member variables to be modified.
* Using `mutable` with lambdas is less common in practice, but it is useful for modifying captured values without affecting the original variable.