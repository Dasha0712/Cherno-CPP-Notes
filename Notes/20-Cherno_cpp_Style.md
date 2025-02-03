# Understanding Logging Class in C++ (Cherno Style)

## Logging Class Implementation

```cpp
#include<iostream>

class Log
{
public:
    const int LogLevelError = 0;
    const int LogLevelWarning = 1;
    const int LogLevelInfo = 2;

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

int main() {
    std::cout << "Hello log class!" << std::endl;
    Log log;
    
    log.Warn("Hello!");
    log.Info("Hello!");
    log.Error("Hello!");
    
    std::cin.get();
    return 0;
}
```

## Explanation:
- **Encapsulation:** The logging levels are defined inside the `Log` class.
- **Member Variables:** `m_LogLevel` is used to store the current logging level.
- **Logging Methods:**
  - `Error()`, `Info()`, and `Warn()` check against `m_LogLevel` before printing messages.
- **Naming Convention:**
  - Member variables follow `m_variableName` notation for clarity.
- **Code Style:**
  - This follows Cherno’s coding style, emphasizing clean and structured C++ code.
