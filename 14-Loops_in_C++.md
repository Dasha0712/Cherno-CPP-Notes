# Loops in C++

Loops are fundamental constructs in programming used to execute a block of code repeatedly under certain conditions. In C++, there are three primary types of loops:

## 1. `for` Loop

The `for` loop is used when the number of iterations is known beforehand.

### Syntax:

```cpp
for(initialization; condition; increment/decrement) {
    // code block
}
```

### Example:

```cpp
#include <iostream>

int main() {
    for(int i = 0; i < 5; i++) {
        std::cout << "i = " << i << std::endl;
    }
    return 0;
}
```

### When to use:

* When the number of iterations is known.
* Useful for counting loops and iterating over arrays with indices.

---

## 2. `while` Loop

The `while` loop is used when the number of iterations is not known and depends on a condition.

### Syntax:

```cpp
while(condition) {
    // code block
}
```

### Example:

```cpp
#include <iostream>

int main() {
    int i = 0;
    while(i < 5) {
        std::cout << "i = " << i << std::endl;
        i++;
    }
    return 0;
}
```

### When to use:

* When the condition must be checked before executing the loop body.
* Useful when the loop may not run at all if the condition is initially false.

---

## 3. `do-while` Loop

The `do-while` loop is similar to the `while` loop, but it checks the condition after executing the loop body.

### Syntax:

```cpp
do {
    // code block
} while(condition);
```

### Example:

```cpp
#include <iostream>

int main() {
    int i = 0;
    do {
        std::cout << "i = " << i << std::endl;
        i++;
    } while(i < 5);
    return 0;
}
```

### When to use:

* When the loop must run at least once, regardless of the condition.

---

## Loop Control Statements

### `break`

Exits the loop immediately.

### Example:

```cpp
for(int i = 0; i < 10; i++) {
    if(i == 5) break;
    std::cout << i << std::endl;
}
```

### `continue`

Skips the current iteration and continues with the next.

### Example:

```cpp
for(int i = 0; i < 10; i++) {
    if(i % 2 == 0) continue;
    std::cout << i << std::endl;
}
```

---

## Nested Loops

Loops can be nested inside another loop.

### Example:

```cpp
for(int i = 1; i <= 3; i++) {
    for(int j = 1; j <= 2; j++) {
        std::cout << "i = " << i << ", j = " << j << std::endl;
    }
}
```

---

## Infinite Loops

Created when the loop condition never becomes false.

### Example:

```cpp
while(true) {
    // run forever unless a break is used
}
```

Use infinite loops with caution and make sure to include a `break` or exit condition inside.

---

## Summary

| Loop Type  | Condition Check | Use Case                     |
| ---------- | --------------- | ---------------------------- |
| `for`      | Before loop     | Known number of iterations   |
| `while`    | Before loop     | Unknown number of iterations |
| `do-while` | After loop      | Must execute at least once   |

Loops are essential for repetitive tasks, and selecting the right type of loop can make your code more efficient and readable.
