## Explanation of the Code

### Overview:
This C++ program demonstrates **inheritance**, where the `dog` class inherits from the `animal` class. It shows how a derived class can access and modify the properties of its base class.

### Code Breakdown:

```cpp
#include<iostream>
```
- The `#include<iostream>` allows for input and output operations using `std::cout`.

```cpp
class animal {
public:
    int age = 100;
    int weight = 70;
    int height = 200;
```
- The `animal` class has three public attributes: `age`, `weight`, and `height`, initialized with default values.

```cpp
    void sound() {
        std::cout << "Animal sound" << std::endl;
    }
};
```
- The `sound()` method prints "Animal sound" when called.

```cpp
class dog : public animal {
public:
    void show() {
        std::cout << "Age: " << age << std::endl;
        std::cout << "Weight: " << weight << std::endl;
        std::cout << "Height: " << height << std::endl;
    }
};
```
- The `dog` class **inherits** from `animal` using public inheritance (`: public animal`).
- It defines a `show()` method that prints the values of `age`, `weight`, and `height`.

```cpp
int main() {
    animal a;
    dog d;
```
- Two objects are created: `a` (from `animal`) and `d` (from `dog`).

```cpp
    d.age = 99;
    d.weight = 88;
    d.height = 77;
```
- The values of `d`'s attributes (inherited from `animal`) are modified.

```cpp
    d.show();
```
- Calls the `show()` method to display the modified values.

```cpp
    std::cout << a.age << std::endl;
    std::cout << a.weight << std::endl;
    std::cout << a.height << std::endl;
```
- Prints the default values of `a` (animal instance), which remain unchanged.

```cpp
    d.sound();
```
- Calls the inherited `sound()` method from `animal`, printing "Animal sound".

```cpp
    return 0;
}
```
- The program successfully executes and returns `0`.

### Expected Output:
```
Age: 99
Weight: 88
Height: 77
100
70
200
Animal sound
```

### Key Concepts:
1. **Inheritance**: The `dog` class extends `animal`, gaining its properties and methods.
2. **Overriding vs. Inheriting**: The `dog` class does not override any methods but inherits them.
3. **Accessing Parent Class Attributes**: The `dog` object modifies and displays inherited attributes, while the `animal` object retains its default values.

### Improvement Suggestion:
- Use **protected** access specifier for `age`, `weight`, and `height` in the `animal` class to restrict direct access but allow modification in derived classes.

This program is a great example of **basic inheritance in C++**!