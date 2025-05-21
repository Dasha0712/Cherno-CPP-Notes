## Best Visual Studio Setup for C++ Projects

Cherno shares his personal Visual Studio setup routine that he uses across all C++ projects. While these settings might not suit everyone, they offer a solid foundation for clean project organization and easy file management.

### 1. Creating a New Project

* Open Visual Studio → **File > New > Project**.
* Choose **Visual C++ > General > Empty Project**.
* Name your project, e.g., `NewProject`.
* **Location Tip:** Set location to something like `C:\dev\NewProject` (avoid placing inside the user folder).
* Ensure **"Create directory for solution"** is checked.

### 2. Understanding the Default Structure

* Visual Studio creates a `.sln` (solution) file and a `.vcxproj` (project) file.
* Default filters like *Header Files*, *Source Files*, etc., are **virtual folders** and don't exist on disk.

### 3. Using Real Folders

* Enable **Show All Files** in Solution Explorer.
* Right-click → **Add > New Folder** to create real directories (e.g., `src`).
* Move files (e.g., `main.cpp`) into these folders for better organization.

### 4. Filters vs. Folders

* Filters (virtual folders) help organize files in Solution Explorer.
* Real folders help keep the file system organized.
* Changing file locations in Explorer requires manual updates in Visual Studio unless "Show All Files" is enabled.

### 5. Writing and Building Code

* Add a simple `main.cpp` file in the `src` folder:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
```

* Right-click the project → **Build**.

### 6. Understanding Build Output Paths

* By default, Visual Studio:

  * Puts intermediate files (e.g., `.obj`) in `ProjectDir/Debug/`.
  * Places the final `.exe` in `SolutionDir/Debug/`.

This can be confusing and is **not ideal** for larger projects.

### 7. Customizing Output Directories

* Right-click project → **Properties** → **All Configurations** + **All Platforms**.

#### Set Output Directory:

```
$(SolutionDir)bin\$(Platform)\$(Configuration)\
```

#### Set Intermediate Directory:

```
$(SolutionDir)bin\intermediates\$(Platform)\$(Configuration)\
```

* This ensures all executables go to a unified `/bin` folder, and intermediates are neatly tucked away.

### 8. Clean Project Structure

* Clean project: Right-click → **Clean** or manually delete `Debug/` and other generated folders.
* Final structure:

  * `src/` → Source code
  * `bin/` → All build outputs
  * Project and solution files are tidy

### 9. Macro References

* To inspect Visual Studio macros like `$(SolutionDir)`:

  * Go to **Edit > Macros > View Macros** to confirm they end with backslashes, avoiding double slashes.

### Summary

This setup makes it easier to:

* Share projects across devices
* Manage multiple projects in one solution
* Keep build output organized

Use these settings as a base template for all new C++ projects in Visual Studio. Cherno recommends them for a smoother development experience.
