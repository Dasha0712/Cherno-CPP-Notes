# **Const Usage in C++**

The `const` keyword in C++ can be used in various ways to indicate that a variable, pointer, or reference is constant (its value cannot be modified). Below are different use cases of `const` in C++.

---

## **1. Constant Variable**
### **Syntax:**
```cpp
const int num = 10;
```
### **Explanation:**
- The variable `num` is constant, and its value cannot be changed after initialization.

---

## **2. Constant Pointer**
### **Syntax:**
```cpp
int num = 10;
int* const ptr = &num; // Constant pointer to an integer
```
### **Explanation:**
- `ptr` cannot point to any other memory address, but the value stored at `num` can be modified.

---

## **3. Pointer to Constant**
### **Syntax:**
```cpp
const int* ptr = &num; // Pointer to a constant integer
```
### **Explanation:**
- You cannot change the value stored at `num` through `ptr`, but `ptr` can point to different locations.

---

## **4. Constant Pointer to Constant**
### **Syntax:**
```cpp
const int* const ptr = &num; // Constant pointer to a constant integer
```
### **Explanation:**
- Neither the pointer `ptr` nor the value it points to can be changed.

---

## **5. Constant Reference**
### **Syntax:**
```cpp
const int& ref = num; // Constant reference to an integer
```
### **Explanation:**
- The reference `ref` cannot modify the value of `num`.

---

## **6. Constant Member Function**
### **Syntax:**
```cpp
class MyClass {
public:
    int x;
    void printValue() const {
        std::cout << x << std::endl;
    }
};
```
### **Explanation:**
- The `const` at the end of the member function ensures that the function does not modify any member variables of the class.

---

## **7. Constant Array**
### **Syntax:**
```cpp
const int arr[] = {1, 2, 3, 4};
```
### **Explanation:**
- You cannot modify the elements of `arr` after initialization.

---

## **8. Constant Pointer to Constant Array**
### **Syntax:**
```cpp
const int* const ptrArr = arr; // Constant pointer to a constant array
```
### **Explanation:**
- The pointer `ptrArr` cannot point to a different array, and the values of the array elements cannot be modified.

---

## **9. Constant in Function Arguments**
### **Syntax:**
```cpp
void printValue(const int num) {
    std::cout << num << std::endl;
}
```
### **Explanation:**
- The parameter `num` is constant, meaning the function cannot modify it.

---

## **10. Constant Class Member Variable**
### **Syntax:**
```cpp
class Example {
public:
    const int x;
    Example(int val) : x(val) {}
};
```
### **Explanation:**
- `x` must be initialized in the constructor initialization list and cannot be modified later.

---

## **11. Constant Return Type**
### **Syntax:**
```cpp
const int getValue() {
    return 10;
}
```
### **Explanation:**
- The return value of the function is constant, meaning it cannot be modified after being returned.

---

## **12. Constant Objects**
### **Syntax:**
```cpp
const MyClass obj;
```
### **Explanation:**
- The object `obj` is constant, meaning its member variables cannot be modified after creation.

---

## **13. Constant Iterator**
### **Syntax:**
```cpp
std::vector<int> vec = {1, 2, 3};
std::vector<int>::const_iterator it = vec.begin();
```
### **Explanation:**
- `const_iterator` ensures that elements pointed to by `it` cannot be modified.

---

## **14. Constant Static Class Member**
### **Syntax:**
```cpp
class MyClass {
public:
    static const int value = 100;
};
```
### **Explanation:**
- `value` is a constant static member, meaning it is shared among all instances and cannot be modified.

---

## **15. Constant Lambda Expressions**
### **Syntax:**
```cpp
auto lambda = []() -> const int {
    return 42;
};
```
### **Explanation:**
- The lambda returns a constant value that cannot be modified.

---

## **Summary of `const` Use Cases:**
| **Use Case** | **Syntax** |
|-------------|-----------|
| Constant Variable | `const int num = 10;` |
| Constant Pointer | `int* const ptr = &num;` |
| Pointer to Constant | `const int* ptr = &num;` |
| Constant Pointer to Constant | `const int* const ptr = &num;` |
| Constant Reference | `const int& ref = num;` |
| Constant Member Function | `void printValue() const;` |
| Constant Array | `const int arr[] = {1, 2, 3};` |
| Constant Pointer to Constant Array | `const int* const ptrArr = arr;` |
| Constant in Function Arguments | `void printValue(const int num);` |
| Constant Class Member Variable | `const int x;` in a class |
| Constant Return Type | `const int getValue();` |
| Constant Objects | `const MyClass obj;` |
| Constant Iterator | `std::vector<int>::const_iterator it = vec.begin();` |
| Constant Static Class Member | `static const int value = 100;` |
| Constant Lambda Expressions | `[]() -> const int { return 42; };` |

Each variation of `const` provides different levels of immutability for variables, pointers, and functions, ensuring safer and more controlled code in C++.

