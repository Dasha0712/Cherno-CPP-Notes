## Making and Working with Libraries in C++ (Static Libraries)

Creating reusable libraries in Visual Studio is essential for modularity and code reuse. Here, we'll look at how to create a static library project and link it to an executable project.

---

### 🧱 Creating Multiple Projects in a Solution

1. Start with an **empty folder** (e.g., `C++/`).

2. Open **Visual Studio** → `File > New Project` → Select `Empty Project` under Visual C++.

   * Name the project `Game` (this will be your main executable).
   * Ensure `Create directory for solution` is **checked**.

3. To add another project (library):

   * Right-click the **Solution** → `Add > New Project` → again select `Empty Project`.
   * Name it `Engine` (this will be your library).

4. Set project types:

➡️ **Game Project (Executable)**
Right-click `Game` → `Properties` → `Configuration Properties > General > Configuration Type`:

```
Application (.exe)
```

➡️ **Engine Project (Static Library)**
Right-click `Engine` → `Properties` → `Configuration Properties > General > Configuration Type`:

```
Static Library (.lib)
```

Make sure this is set for **All Configurations** and **All Platforms**.

---

### 🔧 Writing Some Code

Create source folders and files:

#### In `Engine` project:

Create `Source` folder → Add files:

```cpp
// Engine.h
#pragma once
namespace Engine {
    void PrintMessage();
}

// Engine.cpp
#include "Engine.h"
#include <iostream>

namespace Engine {
    void PrintMessage() {
        std::cout << "Hello World" << std::endl;
    }
}
```

#### In `Game` project:

Create `Source` folder → Add file:

```cpp
// Application.cpp
#include "Engine.h"
#include <iostream>

int main() {
    Engine::PrintMessage();
    std::cin.get();
    return 0;
}
```

---

### ➕ Linking Engine to Game

#### ✅ Recommended: Add as a Project Reference

Right-click `Game` → `Add > Reference` → Tick `Engine` → OK

Benefits:

* Links `Engine.lib` into the executable
* Automatically builds `Engine` if needed
* Creates a proper **dependency graph**
* No need for manual `.lib` management

#### ⚙️ Manual Linking (Alternative)

You can also manually link:

➡️ `Game > Properties > Linker > Input > Additional Dependencies`:

```
Engine.lib
```

➡️ `Game > Linker > General > Additional Library Directories`:

```
[path_to_Engine_output_libs]
```

---

### 📁 Managing Header Files

Rather than this (❌):

```cpp
#include "../../Engine/Source/Engine.h"
```

Use **Include Paths**:

➡️ `Game > Properties > C/C++ > General > Additional Include Directories`:

```
$(SolutionDir)Engine\Source
```

Then you can simply:

```cpp
#include "Engine.h"  // ✅ Clean and portable
```

📌 Tip:

* Use `"header.h"` for your own headers
* Use `<header>` for system or external headers

---

### 🧪 Building and Running

Build `Game` (Visual Studio will build `Engine` first if needed):

```
Hello World
```

Final `.exe` output location:

```
[SolutionDir]/Game/Debug/Game.exe
```

Copy and run this `.exe` standalone — no DLLs required (static linking).

---

### 📦 How Static Linking Works

* When you build `Engine`, it produces `Engine.lib`
* This `.lib` is linked into the `Game.exe`
* The result is **one standalone executable** with all the code embedded

This method is ideal for:

* Portability
* Distribution
* Simplicity in small to medium-sized projects

---

### ✅ Summary

* Create multiple projects in a single solution
* Set your library to `Static Library (.lib)`
* Use project references to auto-manage linking and builds
* Use include paths to simplify header inclusion

🎯 Static linking means everything is packaged into the `.exe` — clean and self-contained.

---

📦 Next Up: Dynamic libraries (.dll), runtime linking, and how they differ from static linking.
