After compiling, the linking process happens. The linker finds and connects all functions and symbols together.

* Every `.cpp` file is compiled into a separate object file, also known as a translation unit. The linker combines all these object files into a single executable.

* Even if the entire program is written in one file, the application still needs to know the entry point (i.e., the `main` function). When you run the application, the runtime library jumps to the `main` function to begin execution. The linker ensures this entry point and all references are properly resolved.

### Example: `main.cpp`

```cpp
#include <iostream>
void log(const char* message)
{
  std::cout << message << std::endl;
}
int multiply(int a, int b)
{
  log("multiply");
  return a * b;
}
```

If you build this without a `main()` function, you'll get a linking error because the application requires an entry point.

**To fix this**, go to:
`Project Properties` → `General` → `Configuration Type` → select `Application (.exe)`

Then in the linker section:
`Linker` → `Advanced` → `Entry Point` → you can specify a custom entry point if needed.

### Completing the code:

```cpp
#include <iostream>
void log(const char* message)
{
  std::cout << message << std::endl;
}
int multiply(int a, int b)
{
  log("multiply");
  return a * b;
}
int main()
{
  std::cout << multiply(5, 8) << std::endl;
}
```

### Moving `log` to a separate file `log.cpp`:

```cpp
#include <iostream>
void log(const char* message)
{
  std::cout << message << std::endl;
}
```

Then in `main.cpp`, just declare the function:

```cpp
#include <iostream>
void log(const char* message);
int multiply(int a, int b)
{
  log("multiply");
  return a * b;
}
int main()
{
  std::cout << multiply(5, 8) << std::endl;
}
```

### Linking Errors Explained

**Unresolved External Symbol** occurs when the linker can’t find a symbol it expects.

1. **Changed function name**: If `log` in `log.cpp` becomes `logr`, compiling `main.cpp` works, but building causes a linking error.

2. **Unused function**: If `log("multiply")` is commented out in `main.cpp`, there's no error because the linker doesn't need `log`.

3. **Indirect call not used**: If `multiply` is never called, but it's not `static`, the linker assumes it could be used in another file and still needs `log`. Mark `multiply` as `static` to restrict it to the current translation unit.

4. **Return type mismatch**: If `log` is defined as returning `int` instead of `void`, linker errors arise due to signature mismatch.

5. **Parameter mismatch**: If the parameter type of `log` changes, linking fails.

6. **Duplicate symbols**: Two functions with the same name and signature in different files cause linker confusion. In the same file, the compiler catches this.

### Using a Header File

Create `log.h` and move the function into it:

```cpp
#include <iostream>
inline void log(const char* message)
{
  std::cout << message << std::endl;
}
```

In `log.cpp`:

```cpp
#include "log.h"
void initlog()
{
  log("multiply");
}
```

In `main.cpp`, just include the header:

```cpp
#include "log.h"
int main()
{
  log("main");
}
```

Using `inline` allows the compiler to copy the definition directly into translation units that include the header, avoiding multiple definitions.

