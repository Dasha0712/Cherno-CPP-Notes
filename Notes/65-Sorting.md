# Sorting in C++

## Introduction
Sorting is a fundamental operation in programming that helps in arranging data in a specific order, such as ascending or descending. The C++ Standard Library provides the `std::sort()` function, which is efficient and easy to use.

---

## Example: Sorting in Different Ways

```cpp
#include<iostream>
#include<functional>
#include<vector>
#include<algorithm>

int main()
{
    std::vector<int> values = {9, 7, 3, 10, 8, 2, 1, 4, 5, 6};
    
    // Sorting in ascending order
    std::sort(values.begin(), values.end());
    std::cout << "Ascending Order:" << std::endl;
    for(int value : values)
    {
        std::cout << value << std::endl;
    }

    // Sorting in descending order
    std::sort(values.begin(), values.end(), std::greater<int>());
    std::cout << "Descending Order:" << std::endl;
    for(int value : values)
    {
        std::cout << value << std::endl;
    }

    // Custom sorting: Keep '1' at the last position and sort in descending order
    std::sort(values.begin(), values.end(), [](int a, int b)
    {
        if (a == 1) return false; // Always place '1' at the end
        if (b == 1) return true;
        return a > b; // Descending order for other elements
    });
    
    std::cout << "Custom Order (Descending but '1' at last):" << std::endl;
    for(int value : values)
    {
        std::cout << value << std::endl;
    }
}
```

---

## Explanation
### 1. **Ascending Order**
   - `std::sort(values.begin(), values.end());`
   - This sorts the vector in increasing order.

### 2. **Descending Order**
   - `std::sort(values.begin(), values.end(), std::greater<int>());`
   - This sorts the vector in decreasing order using `std::greater<int>()`.

### 3. **Custom Sorting**
   - Uses a **lambda function** to define a custom sorting rule.
   - Always places `1` at the end.
   - Sorts the rest of the values in descending order.

---

## Key Takeaways
| Sorting Type         | Syntax |
|----------------------|------------------------------------------------|
| **Ascending Order**  | `std::sort(values.begin(), values.end());`  |
| **Descending Order** | `std::sort(values.begin(), values.end(), std::greater<int>());` |
| **Custom Sorting**   | `std::sort(values.begin(), values.end(), [](int a, int b){ ... });` |

---

## More Resources
For more details, visit [cppreference](https://en.cppreference.com/w/).

