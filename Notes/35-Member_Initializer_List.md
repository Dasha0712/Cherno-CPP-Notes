# Understanding Member Initializers in C++

## 1. Without Member Initializer

```cpp
#include<iostream>
class example {
public:
    example() {
        std::cout << " created an entity" << std::endl;
    }
    example(int x) {
        std::cout << "created an entity with " << x << std::endl;
    }
};

class Entity {
private:
    int m_value;
    int m_score;
    example ex;

public:
    Entity() {
        ex = example(9090); // Creates an extra temporary object before assignment
        m_value = 100;
        m_score = 999;
    }
};

int main() {
    Entity e1;
}
```

### Explanation:
- The constructor of `Entity` creates an `example` object first (default constructor) and then assigns another `example(9090)`, leading to two object creations.
- This is inefficient. Instead, we should use **member initializer lists**.

---

## 2. With Member Initializer (Better Approach)

```cpp
#include<iostream>
class example {
public:
    example() {
        std::cout << " created an entity" << std::endl;
    }
    example(int x) {
        std::cout << "created an entity with " << x << std::endl;
    }
};

class Entity {
private:
    int m_value;
    int m_score;
    example m_ex;

public:
    Entity()
        : m_value(8787), m_score(3443), m_ex(example(8)) // Order of initialization matters!
    {
    }
};

int main() {
    Entity e1;
}
```

### Explanation:
- **Member initializer lists** ensure that the members are initialized directly rather than assigned after default construction.
- The order of initialization follows the **declaration order** in the class, not the order in the initializer list.
- More efficient than the first approach as it avoids unnecessary object creation.
