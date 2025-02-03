# Understanding References in C++

## Code Example

```cpp
#include <iostream>
#define print(x) std::cout << x << std::endl;

int main() {
    int a = 10;
    int b = 99;
    int& ref = a; // ref is now an alias for 'a'
    ref = b;      // assigns the value of 'b' to 'a', NOT changing the reference

    print(a); // Output: 99
    print(b); // Output: 99
}
```

## Explanation
1. `int& ref = a;`
   - `ref` is a reference to `a`, meaning any modification to `ref` will directly affect `a`.
2. `ref = b;`
   - This does **not** make `ref` refer to `b`. Instead, it assigns the value of `b` to `a`.
3. **Final Values:**
   - `a` becomes `99` because `ref = b;` updates `a`.
   - `b` remains `99`.

## Key Takeaways
✅ **References act as aliases**, not separate variables.
✅ **Once a reference is assigned, it cannot be changed to refer to another variable.**
✅ **Assignment to a reference modifies the original variable.**