# Function Pointers and Lambda Expressions in C++

## Problem: Using Function Pointers

```cpp
#include<iostream>
#include<vector>

void printvalue(int value)
{
    std::cout << "value: " << value << std::endl;
}

void foreach(const std::vector<int>& values, void(*func)(int))
{
    for(int value : values)
        func(value);
}

int main()
{
    std::vector<int> values = {1,2,3,4,5};
    foreach(values, printvalue);
}
```

### Why We Should Use Lambda Functions
The above approach requires defining a separate function (`printvalue`). However, this can be cumbersome, especially for small, one-time-use functions. Instead, we can use **lambda expressions**, which allow us to define functions inline.

## Solution: Using Lambda Expressions

```cpp
#include<iostream>
#include<vector>

void foreach(const std::vector<int>& values, void(*func)(int))
{
    for(int value : values)
        func(value);
}

int main()
{
    std::vector<int> values = {1,2,3,4,5};
    foreach(values, [](int value){ std::cout << "value: " << value << std::endl; });
}
```

### Whenever You Need a Function Pointer, Use a Lambda
Lambda expressions simplify code and eliminate the need for function pointers in most cases.

## Function Pointers Explained
If we write `void(*function_pointer)(int)`, `function_pointer` is a pointer to a function.
- When we call `function_pointer(900)`, it is equivalent to calling `printvalue(900)`, assuming `function_pointer` points to `printvalue`.

### Without typedef:
```cpp
#include <iostream>

// Function pointer syntax: return_type(*function_pointer)(parameters)
void helloworld(int x) {
    std::cout << "Hello, World! " << x << std::endl;
}

int main() {
    void(*function_name)(int) = helloworld; // Function pointer
    function_name(90);
    function_name(100);
}
```

### With typedef:
```cpp
#include <iostream>

// typedef return_type(*new_type)(parameter);
typedef void(*function_pointer)(int);

void helloworld(int x) {
    std::cout << "Hello, World! " << x << std::endl;
}

int main() {
    function_pointer fn = helloworld; // `fn` points to `helloworld`
    fn(90);
    fn(100);
}
```

### Why Use Lambda Instead of Function Pointers?
Lambda expressions make code more concise and readable, avoiding unnecessary function declarations. Whenever you need a function pointer, consider using a lambda instead.

## Capturing Variables in Lambda Expressions

```cpp
#include<iostream>
#include<vector>
#include<functional>

void foreach(const std::vector<int>& values, const std::function<void(int)>& func)
{
    for(int value : values)
        func(value);
}

int main()
{
    std::vector<int> values = {1,2,3,4,5};
    int a = 100;
    auto lambda = [a](int value){ std::cout << "value: " << value << ", captured a: " << a << std::endl; };
    
    /*
    If we try to access `a` in a separate function:

    void func()
    {
        std::cout << a << std::endl;
    }
    int main()
    {
        int a = 100;
        func();
    }
    // ---> This will cause an error because `a` is not in the scope of `func`
    */

    // Capturing `a` in a lambda allows access to its value.
    foreach(values, lambda);
}
```

### Why Use Captures in Lambda?
Captures allow lambda functions to access variables from their enclosing scope. Without captures, the lambda cannot access `a`, leading to a scope error.

## Syntax Box: Function Pointer Syntax

### Without typedef:
```cpp
return_type(*function_pointer)(parameters);
```

### With typedef:
```cpp
typedef return_type(*new_type)(parameter);
new_type function_pointer = address_of_function;
```

For more info, visit: [C++ Lambda Expressions](http://en.cppreference.com/w/cpp/language/lambda)
