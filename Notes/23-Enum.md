# Log System Documentation

## Overview
This project consists of a simple logging system implemented in C++. It is inspired by The Cherno's video series and consists of two files:
- `log.h` (Header file)
- `main.cpp` (Main source file)

The project also demonstrates the **concept of enums** in C++ by defining two different enumerations:
- `Log::Level` inside the `Log` class (for logging levels)
- `numbers` (a basic enum example in `main.cpp`)

**Note:** Cherno mentioned that this is a bad way of writing a logging program. The implementation lacks flexibility, and a better approach would involve using a dedicated logging framework or improving the design.

## log.h (Header File)
```cpp
#ifndef LOG_H
#define LOG_H

#include<iostream>

class Log
{
public:
    enum Level
    {
        LogLevelError = 0, 
        LogLevelWarning = 1, 
        LogLevelInfo = 2
    };

private:
    int m_LogLevel = LogLevelInfo;

public:
    void SetLevel(int level)
    {
        m_LogLevel = level;
    }
    void Error(const char* message)
    {
        if (m_LogLevel >= LogLevelError)
            std::cout << "[ERROR]: " << message << std::endl;
    }
    void Info(const char* message)
    {
        if (m_LogLevel >= LogLevelInfo)
            std::cout << "[INFO]: " << message << std::endl;
    }
    void Warn(const char* message)
    {
        if (m_LogLevel >= LogLevelWarning)
            std::cout << "[WARNING]: " << message << std::endl;
    }
};

#endif // LOG_H
```
### Explanation
- The `Log` class contains an `enum Level` to define log levels.
- The private member `m_LogLevel` stores the current logging level.
- `SetLevel(int level)`: Sets the logging level.
- `Error(const char* message)`, `Info(const char* message)`, `Warn(const char* message)`: Display messages based on the current logging level.

---

## main.cpp (Main Source File)
```cpp
#include<iostream>
#include "log.h"

enum numbers
{
    x, y, z
};

int main() {
    numbers a = x;
    std::cout << "Hello log class!" << std::endl;

    Log log;
    // log.SetLevel(log.LogLevelWarning); // Uncomment to set warning level
    log.Warn("Hello!");
    log.Info("Hello!");
    log.Error("Hello!");
    
    std::cin.get();
    return 0;
}
```
### Explanation
- The `numbers` enum is a simple demonstration of enums in C++.
  - It defines three values: `x`, `y`, and `z`.
  - A variable `a` is initialized with `x`.
- The program prints "Hello log class!" to the console.
- A `Log` object is created.
- The `Warn`, `Info`, and `Error` functions are called to demonstrate logging.
- The `std::cin.get();` keeps the console open until user input.

---

## Notes
- The logging level can be modified using `SetLevel()`.
- Uncomment `log.SetLevel(log.LogLevelWarning);` to change the log level to Warning.
- Messages will only be displayed if the log level is equal to or higher than the function’s log level.
- The `numbers` enum is an example of how enums can be used in C++ programs.
- **Cherno pointed out that this is a bad way of writing a logging program, and improvements should be made for better design and flexibility.**

This implementation provides insights into both logging and enumeration concepts in C++!

