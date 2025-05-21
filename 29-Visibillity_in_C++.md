## Visibility in C++

Visibility is a concept in object-oriented programming that defines **who can see, use, or access members (variables or methods) of a class**. It does **not affect program performance**—it exists purely to help developers write cleaner, more organized, and more maintainable code.

### Key Points:

* Visibility is **only for humans**, not for the computer or CPU. It does not change how the program runs.
* Helps enforce correct usage of classes and avoids accidental misuse.

### Visibility Modifiers in C++

C++ has **three visibility modifiers**:

1. `private`
2. `protected`
3. `public`

> Note: Unlike Java or C#, C++ **only** has these three. No `internal` or default modifier like in other languages.

---

### 1. `private`

* Members are only accessible **inside the same class**.
* Even derived (sub) classes **cannot access** private members.

```cpp
class Entity {
    int x, y; // private by default in class
};
```

This is **equivalent to**:

```cpp
class Entity {
private:
    int x, y;
};
```

* If using `struct`, default visibility is `public`:

```cpp
struct Entity {
    int x, y; // public by default
};
```

* Only the class (or its **friends**) can access private members.
* You can **not access** private members from:

  * Main function
  * Subclasses
  * Any other external function or class

Example:

```cpp
class Entity {
private:
    int x;
public:
    Entity() { x = 0; }
    void Print() {}
};

class Player : public Entity {
    Player() {
        // x = 5; // ❌ Error: x is private in Entity
    }
};

int main() {
    Entity e;
    // e.x = 5; // ❌ Error: x is private
    return 0;
}
```

#### Friends (Advanced Topic)

A `friend` is a special keyword in C++ that allows another class or function to access private members.

> Will be covered in a future video.

---

### 2. `protected`

* Same as private **except**:

  * Accessible **by derived classes**
  * Still not accessible from outside (e.g. `main()`)

```cpp
class Entity {
protected:
    int x;
};

class Player : public Entity {
    Player() {
        x = 10; // ✅ Allowed: x is protected
    }
};

int main() {
    Player p;
    // p.x = 5; // ❌ Not allowed
}
```

---

### 3. `public`

* Members are accessible **from anywhere**:

  * Inside the class
  * In derived classes
  * In `main()` or other external code

```cpp
class Entity {
public:
    int x;
};

int main() {
    Entity e;
    e.x = 5; // ✅ Allowed
}
```

---

### Why Use Visibility?

If visibility doesn’t affect performance, **why use it?**

* Helps you and other developers understand how a class is intended to be used.
* Prevents accidental misuse of internal implementation details.
* Makes code **easier to maintain** and **less error-prone**.
* Encourages **proper abstraction** and **encapsulation**.

#### Example: Moving a UI Button

Suppose we have a button with `x` and `y` position:

```cpp
class Button {
private:
    int x, y;

public:
    void SetPosition(int newX, int newY) {
        x = newX;
        y = newY;
        Refresh(); // Updates display
    }

    void Refresh() {
        // Redraw button on screen
    }
};
```

* If `x` and `y` were public, someone might set them directly:

  ```cpp
  button.x = 10; // ❌ Doesn't refresh the UI
  ```
* By making them `private`, users **must** call `SetPosition()`, ensuring consistent behavior.

---

### Visibility = Communication

* Visibility modifiers **communicate intent**.

  * `private` → "You shouldn’t touch this unless you’re inside this class."
  * `public` → "This is safe to use from outside."

### Common Misconceptions

* Making everything public = ❌ Bad idea
* Making everything private with public getters/setters = ❌ Also not ideal (too rigid)

  * Avoid **always** using a specific pattern—there are exceptions!

### Summary

* Visibility in C++ is a tool **for developers**, not computers.
* It helps enforce proper usage, maintainability, and encapsulation.
* Use visibility wisely to create better software architecture.

---

Cherno encourages developers to think critically about visibility—don’t blindly follow rules like "always make everything private with getters/setters." Consider what's appropriate for your class and how it’s meant to be used.

> "Even if you're working alone, visibility helps your future self understand your own code."

---

### Access Table

| Access Modifier | Accessible within Class | Accessible in Derived Classes | Accessible Outside the Class | Notes                             |
| --------------- | ----------------------- | ----------------------------- | ---------------------------- | --------------------------------- |
| `private`       | ✅ Yes                   | ❌ No                          | ❌ No                         | Only class and friends can access |
| `protected`     | ✅ Yes                   | ✅ Yes                         | ❌ No                         | Accessible in subclass hierarchy  |
| `public`        | ✅ Yes                   | ✅ Yes                         | ✅ Yes                        | Fully accessible                  |
| `friend`        | ✅ Yes (granted access)  | ✅ Yes (if declared friend)    | ✅ Yes (if declared friend)   | Special access keyword            |
