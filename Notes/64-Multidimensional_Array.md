## Multidimensional Arrays in C++

### Example 1: Using Dynamic Memory for a 1D Array and 2D Pointer Array
```cpp
#include<iostream>

int main()
{
    int* array = new int[50]; // Allocate dynamic memory for a 1D array
    int** a2d = new int*[50]; // Allocate dynamic memory for a 2D array pointer

    array[0] = nullptr; // Here it is showing an error because it has to store an integer
    a2d[0] = nullptr; // Here we are storing an integer pointer

    // array[0] means dereferencing. Let me explain:
    // array = starting address in heap for 50 integers
    // (array[0] = nullptr) == (address of the first integer = nullptr)
    // (a2d[0] = nullptr) == (address of another pointer which is pointing to the first integer address = nullptr)
}
```

### What is a 2D Array?
```cpp
#include<iostream>

int main()
{
    int** a2d = new int*[50]; // Allocate dynamic memory for a 2D array pointer
    for(int i = 0; i < 50; i++){
        a2d[i] = new int[50]; // This is what a 2D array is
    }

    a2d[0][0] = 909; // Assigning value to a 2D array element
}
```

### What is a 3D Array?
```cpp
#include<iostream>

int main()
{
    int*** a3d = new int**[50]; // Allocate memory for 3D array pointer
    for(int i = 0; i < 50; i++)
    {
        a3d[i] = new int*[50];
        for(int j = 0; j < 50; j++)
        {
            a3d[i][j] = new int[50]; // Allocate memory for each 1D array inside the 2D structure
            // int** ptr = a3d[i];
            // ptr[j] = new int[50];
        }
    }
    a3d[4][5][6] = 8099; // Assigning a value to a 3D array element
}
```

### Deleting Multidimensional Arrays

To properly delete dynamically allocated arrays, you must free the memory in reverse order of allocation.

#### Deleting a 1D Array:
```cpp
delete[] array;
```

#### Deleting a 2D Array:
```cpp
for (int i = 0; i < 50; i++) {
    delete[] a2d[i];
}
delete[] a2d;
```

#### Deleting a 3D Array:
```cpp
for (int i = 0; i < 50; i++) {
    for (int j = 0; j < 50; j++) {
        delete[] a3d[i][j];
    }
    delete[] a3d[i];
}
delete[] a3d;
```

### Why Can't We Delete Multidimensional Arrays Like a Normal Heap?

Multidimensional arrays require nested loops to free memory because each level of the array points to additional memory allocations. Simply calling `delete[]` on the base pointer won't free all allocated memory. Failure to correctly delete all nested allocations leads to memory leaks.

