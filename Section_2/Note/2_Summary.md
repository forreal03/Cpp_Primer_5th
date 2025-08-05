# Chapter 2. Variables and Basic Types

## Contents
- 2.1 Primitive Built-in Types  
- 2.1.1 Arithmetic Types  
- 2.1.2 Type Conversions  
- 2.1.3 Literals  
- 2.2 Variables  
  - 2.2.1 Variable Definitions  
  - 2.2.2 Declarations vs. Definitions  
  - 2.2.3 Identifiers  
  - 2.2.4 Scope of a Name  
- 2.3 Compound Types  
  - 2.3.1 References  
  - 2.3.2 Pointers  
  - 2.3.3 Declarator Syntax  
- 2.4 `const` Qualifier  
- 2.5 Dealing with Types  
  - 2.5.1 Type Aliases  
  - 2.5.2 `auto` Type Specifier  
  - 2.5.3 `decltype` Type Specifier  
- 2.6 Defining Our Own Data Structures  
  - 2.6.1 `Sales_data` (Plain Struct)  
  - 2.6.2 Using `Sales_data`  
  - 2.6.3 Writing Header Files  

---

## 2.1 Primitive Built-in Types
C++ offers a set of fundamental types:
- **Integral types**: `bool`, `char`, `wchar_t`, `char16_t`, `char32_t`, `short`, `int`, `long`, `long long`
- **Floating-point types**: `float`, `double`, `long double`
- **`void`**: no values, used for functions that return nothing

### 2.1.1 Arithmetic Types
- The standard guarantees minimum sizes; actual sizes vary by implementation.
- Common advice: use `int` for integers and `double` for floating-point.  
- Avoid using `char`/`bool` in arithmetic expressions unless you know what you’re doing.

### 2.1.2 Type Conversions
- Implicit conversions:
  - Zero → `false`; non-zero → `true`.
  - Floating-point → integer: truncates toward zero.
  - Integer → floating-point: exact if value is representable; otherwise rounded.

### 2.1.3 Literals
- **Integer literals**: decimal, octal (`0` prefix), hexadecimal (`0x` prefix); suffixes `u/U`, `l/L`, `ll/LL`.
- **Floating-point literals**: e.g. `3.14`, `2e10`; suffixes `f/F` (float), `l/L` (long double).
- **Character literals**: `'a'`, wide `L'a'`; string literals: `"text"`, wide `L"text"`.
- **Boolean**: `true`, `false`; **null pointer**: `nullptr`.

---

## 2.2 Variables
A variable is an object with a type that determines its storage and the operations you can perform.

### 2.2.1 Variable Definitions
```cpp
int sum = 0, value, units_sold = 0;
Sales_item item;
std::string book("0-201-78345-X");
```
- All names share the same base type.
- Initializers are optional (but uninitialized built-ins have indeterminate value).

### 2.2.2 Declarations vs. Definitions
- **Declaration**: makes a name known without allocating storage.  
  ```cpp
  extern int i;  // declaration
  ```
- **Definition**: allocates storage (and may initialize).  
  ```cpp
  int i = 42;    // definition
  ```

### 2.2.3 Identifiers
- Must begin with a letter or underscore (`_`), followed by letters, digits, or underscores.

### 2.2.4 Scope of a Name
- **Block scope**, **function scope**, **namespace scope**, **global scope**.
- Inner (nested) scopes can hide names in outer scopes; use carefully to avoid confusion.

---

## 2.3 Compound Types
Types built from other types.

### 2.3.1 References
An alias for another object. Must be initialized when declared and cannot be reseated.
```cpp
int ival = 1024;
int &r = ival;  // r is another name for ival
```

### 2.3.2 Pointers
Store the address of another object. Use `*` to dereference, `&` to take address.
```cpp
int ival = 1024;
int *pi = &ival;
int **ppi = &pi;
```

### 2.3.3 Declarator Syntax
Read declarations right-to-left, applying the closest operator to the identifier first.

---

## 2.4 `const` Qualifier
Marks an object as immutable after initialization.
```cpp
const int bufSize = 512;  // cannot be changed
```
- **Top-level `const`** vs. **low-level `const`**  
- **`constexpr`** for values that must be constant at compile time.

---

## 2.5 Dealing with Types
Techniques to simplify or deduce types.

### 2.5.1 Type Aliases
```cpp
typedef double wages;
using SI = Sales_item;
```
Helps document intent and shorten long type names.

### 2.5.2 `auto` Type Specifier
Let the compiler deduce the type from the initializer.
```cpp
auto total = val1 + val2;
auto i = 0, *p = &i;
```

### 2.5.3 `decltype` Type Specifier
Deduces the type of an expression without evaluating it.
```cpp
decltype(f()) sum = x;         // type returned by f()
decltype(ci) x = 0;            // if ci is const int, x is const int
```

---

## 2.6 Defining Our Own Data Structures
Use `struct` or `class` to group related data.

### 2.6.1 Defining `Sales_data`
```cpp
struct Sales_data {
  std::string bookNo;
  unsigned units_sold = 0;
  double revenue = 0.0;
};
```

### 2.6.2 Using `Sales_data`
- Read, combine, and print transaction records using member and non-member functions.

### 2.6.3 Writing Header Files
Guard against multiple inclusion:
```cpp
#ifndef SALES_DATA_H
#define SALES_DATA_H

#include <string>
struct Sales_data { … };

#endif // SALES_DATA_H
```

---

## Chapter Summary
- Covered built-in types, conversions, and literals.  
- Defined variables, scope, and linkage.  
- Introduced references, pointers, and declarator syntax.  
- Explained `const`/`constexpr`.  
- Showed type aliases, `auto`, and `decltype`.  
- Defined simple data structures with header guards.

## Defined Terms
Type, object, declaration, definition, scope, lvalue, rvalue, initializer, reference, pointer, `const`, `constexpr`, `typedef`, `auto`, `decltype`, header guard.
