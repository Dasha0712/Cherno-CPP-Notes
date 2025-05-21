# Condition and Branches in C++

Control flow is an essential part of any programming language. In C++, we control the flow of execution using **conditions** and **branches**. These allow the program to make decisions and execute different code blocks based on those decisions.

## 1. `if` Statement

The `if` statement is used to execute a block of code only if a specified condition is true.

### Syntax:

```cpp
if (condition) {
    // code to execute if condition is true
}
```

### Example:

```cpp
int a = 10;
if (a > 5) {
    std::cout << "a is greater than 5" << std::endl;
}
```

## 2. `if-else` Statement

The `if-else` structure adds an alternative block of code if the condition is false.

### Syntax:

```cpp
if (condition) {
    // true block
} else {
    // false block
}
```

### Example:

```cpp
int a = 3;
if (a > 5) {
    std::cout << "a is greater than 5" << std::endl;
} else {
    std::cout << "a is 5 or less" << std::endl;
}
```

## 3. `if-else if-else` Ladder

Used when you want to test multiple conditions.

### Example:

```cpp
int a = 10;
if (a < 5) {
    std::cout << "Less than 5" << std::endl;
} else if (a == 10) {
    std::cout << "Equals 10" << std::endl;
} else {
    std::cout << "Other value" << std::endl;
}
```

## 4. `switch` Statement

Use `switch` when you want to compare the value of a variable against multiple constants.

### Syntax:

```cpp
switch (expression) {
    case constant1:
        // code
        break;
    case constant2:
        // code
        break;
    default:
        // code
}
```

### Example:

```cpp
int day = 3;
switch (day) {
    case 1:
        std::cout << "Monday";
        break;
    case 2:
        std::cout << "Tuesday";
        break;
    case 3:
        std::cout << "Wednesday";
        break;
    default:
        std::cout << "Another day";
        break;
}
```

### Notes:

* `break` is important to prevent fall-through to the next case.
* `default` is optional but recommended.

## 5. Ternary Operator `?:`

A short form of `if-else` statement.

### Syntax:

```cpp
condition ? expression_if_true : expression_if_false;
```

### Example:

```cpp
int a = 10;
std::string result = (a > 5) ? "greater" : "not greater";
std::cout << result;
```

## 6. Boolean Expressions

Conditions are typically based on **boolean expressions**, which evaluate to `true` or `false`.

### Comparison Operators:

* `==` : equal
* `!=` : not equal
* `>`  : greater than
* `<`  : less than
* `>=` : greater than or equal to
* `<=` : less than or equal to

### Logical Operators:

* `&&` : logical AND
* `||` : logical OR
* `!`  : logical NOT

### Example:

```cpp
if ((x > 10 && y < 5) || !flag) {
    // do something
}
```

## 7. Nested Conditions

You can nest `if` or `switch` statements inside each other.

### Example:

```cpp
int age = 20;
bool hasLicense = true;

if (age >= 18) {
    if (hasLicense) {
        std::cout << "Can drive";
    } else {
        std::cout << "Needs license";
    }
} else {
    std::cout << "Too young to drive";
}
```

## Best Practices

* Always use curly braces `{}` even for single-line statements (to avoid logic bugs).
* Keep conditions readable; avoid deep nesting where possible.
* Use `switch` over long `if-else` chains when comparing a variable to constants.
* Comment your logic for complex conditions.

## Summary Table

| Feature           | Use Case                                 |
| ----------------- | ---------------------------------------- |
| `if`              | Simple condition                         |
| `if-else`         | One condition, two branches              |
| `if-else if`      | Multiple conditions                      |
| `switch`          | Comparing one variable against constants |
| Ternary `?:`      | Short conditional assignment             |
| Boolean operators | Build complex logical expressions        |
