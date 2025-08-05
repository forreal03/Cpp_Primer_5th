## 2.3 Compound Types  
Compound types are built from other types—most commonly via pointers, references, and arrays.  

### 2.3.1 References  
A _reference_ is an alias for another object. Once initialized, it cannot be “rebound” to refer to a different object.  
```cpp
int x = 42;      // an int object
int& r = x;      // r is a reference bound to x
r = 100;         // modifies x; now x == 100
```
- **Must** be initialized when declared.  
- Cannot be null.  
- Use when you want function parameters or return values to refer directly to existing objects without copying.

### 2.3.2 Pointers  
A _pointer_ holds the address of an object. You can change which object a pointer points to, and you can point to nothing (nullptr).  
```cpp
int ival = 42;
int* p = &ival;    // p holds address of ival
*p = 99;           // modifies ival; now ival == 99

int j = 123;
p = &j;            // p now points to j
p = nullptr;       // p points to nothing
```
- Use `&` to take an object’s address; use `*` to dereference a pointer.  
- Always initialize pointers; prefer `nullptr` for an empty pointer.

### 2.3.3 Declarator Syntax  
Declarators combine base types with pointers (`*`), references (`&`), and arrays (`[]`). Read them right-to-left, applying the innermost operator first.  
```cpp
int* p;           // p is a pointer to int
int& r = ival;    // r is a reference to int
int a[10];        // a is an array of 10 ints
int (*fp)(double);// fp is a pointer to a function taking double, returning int
```
- Parentheses can change grouping:  
  - `int* p[5];` → p is an array of 5 pointers to int.  
  - `int (*p)[5];` → p is a pointer to an array of 5 ints.

---

## 2.4 `const` Qualifier  
The `const` qualifier makes an object’s value immutable after initialization.  
```cpp
const int BUF_SIZE = 512;  // cannot change later
int const x = 5;           // equivalent
```
- **Top-level const** (the object itself is const) vs. **low-level const** (the pointee is const).  
- You can bind a const reference to a non-const object, but not vice versa.  
- **`constexpr`** indicates a value that must be known at compile time:  
  ```cpp
  constexpr double PI = 3.1415926535;
  ```
- Const correctness is enforced by the compiler; writing to a `const` object is an error.

---

## 2.5 Dealing with Types  
Modern C++ provides tools to simplify and deduce complex types.

### 2.5.1 Type Aliases  
Create a shorthand or document intent:  
```cpp
typedef std::vector<Sales_data> SalesList;   // old style
using SalesList = std::vector<Sales_data>;   // preferred C++11 style
```

### 2.5.2 `auto` Type Specifier  
Let the compiler deduce the type from the initializer. Requires an initializer:  
```cpp
auto cnt = 0;                     // cnt is int
auto p  = &cnt;                   // p is int*
auto v  = someVector.begin();     // v’s iterator type
```
- Reduces verbosity for long or changing types.  
- Forces you to initialize immediately.

### 2.5.3 `decltype` Type Specifier  
Deduces the type of an expression without evaluating it:  
```cpp
int  i = 0;
const int ci = i;
decltype(i)  x = 1;   // x is int
decltype(ci) y = 2;   // y is const int
auto f() -> double;   // decltype(f()) is double
```
- Preserves `const` and reference qualifiers of the expression.  
- Useful when you need the exact type of a complex expression.

---

## 2.6 Defining Our Own Data Structures  
Group related data and behavior using `struct` or `class`.

### 2.6.1 `Sales_data` (Plain Struct)  
A simple example of a value type for book transactions:
```cpp
struct Sales_data {
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;

    // (optional) member functions can go here
};
```
- Default member initializers set sensible defaults.

### 2.6.2 Using `Sales_data`  
Read and combine records:
```cpp
Sales_data item1, item2;
std::cin >> item1.bookNo >> item1.units_sold >> item1.revenue;
std::cin >> item2.bookNo >> item2.units_sold >> item2.revenue;

if (item1.bookNo == item2.bookNo) {
    item1.units_sold += item2.units_sold;
    item1.revenue      += item2.revenue;
    std::cout << item1.bookNo 
              << " total units: " << item1.units_sold
              << " total revenue: " << item1.revenue << '\n';
}
```

### 2.6.3 Writing Header Files  
Keep declarations in a header and guard against multiple inclusion:
```cpp
// Sales_data.h
#ifndef SALES_DATA_H
#define SALES_DATA_H

#include <string>

struct Sales_data {
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue      = 0.0;
};

#endif // SALES_DATA_H
```
- Implementation (.cpp) files include this header.  
- Header guards (`#ifndef`/`#define`/`#endif`) prevent redefinition errors.
