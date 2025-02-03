# Explanation of the Code

## Overview:
This C++ program demonstrates **method overriding**, **virtual functions**, and **polymorphism**. The `Entity` class has a virtual method `GetName1()`, which is overridden in the `player` class.

## Code Breakdown:

```cpp
#include<iostream>
#include<string.h>
```
- `#include<iostream>` is required for input and output operations.
- `#include<string.h>` is not necessary because we are using `std::string` from the standard library.

### Defining the Base Class `Entity`
```cpp
class Entity {
public:
    virtual std::string GetName1() {
        return "Entity";
    }
};
```
- The function `GetName1()` is marked as **virtual**, allowing derived classes to override it.

### Defining the Derived Class `player`
```cpp
class player : public Entity {
public:
    std::string GetName2() {
        return "Dasha";
    }
    std::string GetName1() override {
        return "this is changed entity";
    }
};
```
- `GetName2()` is a new method specific to `player`.
- `GetName1()` overrides the base class method and returns a different string.
- The `override` keyword ensures `GetName1()` correctly overrides a virtual function from the base class.

### Main Function:
```cpp
int main() {
    Entity* e = new Entity();
    std::cout << e->GetName1() << std::endl;
    
    player* p = new player();
    std::cout << p->GetName2() << std::endl;
    
    Entity* entity = p;
    std::cout << entity->GetName1() << std::endl;
    
    std::cin.get();
}
```
- `Entity* e = new Entity();`: Creates an `Entity` object and calls `GetName1()`, printing "Entity".
- `player* p = new player();`: Creates a `player` object and calls `GetName2()`, printing "Dasha".
- `Entity* entity = p;`: Assigns the `player` object to an `Entity*` pointer.
- `entity->GetName1();`: Calls `GetName1()`, but because `GetName1()` is virtual, **it calls `player`'s overridden version**, printing "this is changed entity".

### What Happens Without `virtual`:
If `GetName1()` is **not virtual** in `Entity`:
```cpp
class Entity {
public:
    std::string GetName1() {
        return "Entity";
    }
};
```
Then, even though `entity` points to a `player` object:
```cpp
Entity* entity = p;
std::cout << entity->GetName1() << std::endl;
```
- The **base class method** is called because the type of `entity` is `Entity*`, not `player*`.
- Output would be **"Entity"** instead of "this is changed entity".

## Key Concepts:
1. **Virtual Functions:** Enable dynamic (runtime) method overriding.
2. **Polymorphism:** Calling overridden methods through a base class pointer.
3. **Type Importance:** Without `virtual`, function calls are resolved based on the pointer type, not the actual object type.

## Summary:
- **Using `virtual` allows method overriding**, ensuring correct function execution at runtime.
- **If `virtual` is removed, method calls depend on pointer type, not object type**.
- **Polymorphism is useful when handling objects of derived classes via base class pointers**.

This example showcases **runtime polymorphism**, a key concept in object-oriented programming!
