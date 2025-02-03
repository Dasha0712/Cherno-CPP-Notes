# Understanding Pointers and References in C++

## Code Example

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl;

int main() {
    int a = 10;
    int* ptr = &a;   // Pointer to an integer
    int** ptr2 = &ptr; // Pointer to a pointer

    print(**ptr2); // Output: 10
    print(*ptr);   // Output: 10

    std::cin.get();
}
```

## Explanation
1. `int* ptr = &a;` → `ptr` holds the memory address of `a`.
2. `int** ptr2 = &ptr;` → `ptr2` holds the address of `ptr`, creating a pointer-to-pointer.
3. `**ptr2` dereferences `ptr2` to get `ptr`, then dereferences `ptr` to get `a`'s value.
4. `*ptr` dereferences `ptr` to directly get `a`'s value.

## Difference Between Pointer and Reference
- A **pointer** can be reassigned to another memory location, whereas a **reference** cannot be changed after initialization.
- A pointer can be `nullptr`, but a reference must always refer to a valid object.
- Pointers can be used for complex memory management (like dynamic allocation), while references are simpler and safer.

## Example Showing Pointer Capabilities Over References

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl;

int main() {
    int a = 10, b = 20;
    int* ptr = &a;
    ptr = &b; // Allowed: Pointers can be reassigned

    int& ref = a;
    // ref = &b; // Error: References cannot be reassigned

    print(*ptr); // Output: 20
    print(ref);  // Output: 10
}
```

## Key Takeaways
✅ **Pointers can be reassigned, references cannot.**
✅ **References are safer and easier to use, while pointers offer more flexibility.**
✅ **Pointers can point to `nullptr`, references must always refer to a valid object.**