# 📘 String Literals in C++ — Notes from The Cherno

This guide captures everything The Cherno said in his video on **String Literals in C++**, explained clearly and accessibly. All concepts and insights are included.

---

## 🔤 What is a String Literal?

* A **string literal** is a sequence of characters inside **double quotes**, like this:

  ```cpp
  "Cherno"
  ```
* In C++, a string literal is of type `const char[7]` (not just 6), because it includes:

  * The characters: `C`, `h`, `e`, `r`, `n`, `o`
  * An **extra null terminator character**: `\0`

> `\0` marks the **end** of the string so that functions can detect where it finishes.

* Writing `\0` (null) is **not** the same as `'0'` (character zero) — the null has a numeric value of **zero**, while `'0'` has the ASCII value of **48**.

---

## 🧪 Exploring String Literals in Memory

```cpp
const char* name = "Cherno";
```

* Using a memory view, you can inspect how the string is laid out.
* You'll see the 6 characters followed by a **00 byte** (null terminator).

### Using `strlen`:

* `strlen(name)` returns the length of a C-string up to the first `\0`.
* If `\0` appears **in the middle**, it cuts the string short.

```cpp
const char* name = "Ch\0erno";
strlen(name); // Returns 2, not 6
```

---

## 🔐 `const char*` and Mutability

* String literals are stored in **read-only memory**.
* You should declare them as `const char*` to indicate you don’t plan to modify them.

```cpp
const char* name = "Cherno"; // Correct
```

### Undefined Behavior Warning

```cpp
char* name = "Cherno";
name[2] = 'A'; // ❌ Undefined behavior
```

> Modifying a string literal causes **undefined behavior** because literals are stored in **read-only segments** of the binary.

Some compilers may let this run, others will crash or throw an error.

---

## ⚠️ Compilers and Read-Only Segments

* The memory location of string literals is read-only.
* Cherno shows how compilers like MSVC store the literal in a `.const` segment of the binary.
* Editing the literal in **debug mode** causes a crash.
* In **release mode**, it may silently fail to change the data.

---

## ✅ How to Modify a String Literal Safely

If you want to modify the string:

```cpp
char name[] = "Cherno"; // Copy literal into writable array
name[2] = 'A';           // OK
```

> This copies the literal to the **stack**, making it mutable.

---

## 🧵 Wide and UTF Strings

Besides `char`, C++ supports wide and multi-byte strings:

| Type                | Description                         | Prefix     |
| ------------------- | ----------------------------------- | ---------- |
| `wchar_t`           | Wide character (platform dependent) | `L"text"`  |
| `char16_t`          | UTF-16 string                       | `u"text"`  |
| `char32_t`          | UTF-32 string                       | `U"text"`  |
| UTF-8 (since C++20) | Standard char UTF-8                 | `u8"text"` |

* Example:

  ```cpp
  const wchar_t* wname = L"Cherno";  // Wide string
  const char16_t* u16name = u"Cherno";
  const char32_t* u32name = U"Cherno";
  ```

### Why it matters:

* `wchar_t` is **2 bytes on Windows**, **4 bytes on Linux/macOS**
* `char16_t` is **always** 2 bytes
* `char32_t` is **always** 4 bytes

---

## 🧩 String Literal Operators

From **C++14**, you can append `s` to a string literal to automatically create a `std::string`:

```cpp
using namespace std::string_literals;
auto s = "Cherno"s + "Hello";
```

* `"Cherno"s` creates a `std::string`, enabling string concatenation.

---

## 📝 Raw String Literals

Useful for **multi-line** strings or when escaping characters is messy.

```cpp
const char* text = R"(Line 1
Line 2
Line 3)";
```

* No need for `\n` or escaping quotes.
* Often used for embedding code snippets or paragraphs.

---

## 🧠 Final Insight: How Compilers Handle String Literals

* Cherno demonstrates using **assembly output** that literals are placed in **constant data segments**.
* When using a pointer to a string literal, modifying the string directly is trying to write into a read-only section.
* You must **copy the literal into a local array** if you want to modify it.

---

## ✅ Summary Table

| Concept                | Key Point                                         |
| ---------------------- | ------------------------------------------------- |
| String literal         | Sequence of characters in double quotes           |
| Null terminator (`\0`) | Marks end of string in memory                     |
| `const char*`          | Safe way to store literals                        |
| Modifying literals     | ❌ Undefined behavior                              |
| `char[]` from literal  | ✅ Creates writable copy on stack                  |
| `strlen`               | Counts until `\0`, not full array                 |
| Raw string literals    | Use `R"(...)"` for multi-line text                |
| Wide/UTF string types  | Use `L`, `u`, `U`, `u8` prefixes                  |
| Literal suffixes (`s`) | Enables `std::string` concatenation from literals |

---

Let me know if you’d like visual memory layouts or UTF diagram explanations added!
