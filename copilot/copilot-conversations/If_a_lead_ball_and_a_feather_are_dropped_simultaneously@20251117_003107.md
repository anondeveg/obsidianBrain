---
epoch: 1763332267000
modelKey: gemini-2.5-pro|google
tags:
  - copilot-conversation
topic: Learncpp.com Note Reorganization
---

**user**: If a lead ball and a feather are dropped simultaneously from the same height, which will reach the ground first?
[Context: Notes: -2 Resources Summarized/learncpp.com.md]
[Timestamp: 2025/11/17 00:31:07]

**ai**: Based on general physics principles, the answer depends on the environment in which they are dropped:

-   **In a vacuum (with no air):** Both the lead ball and the feather would reach the ground at the same time. This is because gravity accelerates all objects at the same rate, regardless of their mass or shape.

-   **In the presence of air (like on Earth):** The lead ball will reach the ground first. The feather has a large surface area and very little mass, causing it to be significantly slowed down by air resistance. The lead ball, being dense and heavy, is much less affected by air resistance and will fall faster.

This information is not found in your note [[learncpp.com]], as that note focuses on the C++ programming language.
[Timestamp: 2025/11/17 00:31:15]

**user**: can you reformat this page to make it more organized? do not add anything or correct anything just reorganize
[Context: Notes: -2 Resources Summarized/learncpp.com.md]
[Timestamp: 2025/11/17 00:31:58]

**ai**: Of course, here is a reorganized version of your note [[learncpp.com]]:

# learncpp.com

**Source material**: https://www.learncpp.com/
**Tags**: [[C++]], [[programming]]

---

## Core C++ Concepts

### `main()` Function
When the program is executed, the operating system makes a function call to `main()`. Execution then jumps to the top of `main()`. The statements in `main()` are executed sequentially. Finally, `main()` returns an integer value (usually `0`), and your program terminates.

- You should define your `main()` function at the bottom of your code file, below other functions, and avoid calling it explicitly.

### Datatypes
#### Vectors
- Dynamic array (resizable).
- Arrays are just static arrays.

To create a vector, use the `vector` keyword, and specify the type of values it should store within angle brackets `<>` and then the name of the vector, like: `vector <Type> vectorName`.

**Example:**
```cpp
std::vector<type> Cars;
```

### Loop Types
C++ has 3 loop types:
- **for**
- **while**
    - When you put a semicolon (;) after a while loop it's considered bodyless and will loop forever.
        - We can leverage this to our use by making a while loop that calls a function until it's false.
        ```cpp
        while(runUntilFalse);
        ```
    - Be careful about placing a semicolon after the condition of a while-statement, as it will result in an infinite loop unless the condition has some way to evaluate to false.
- **do while**

### Functions
A function within a function is illegal.
```cpp
// Illegal - will not work
void x(){
	void b(){
	} 
}

// Correct way
void b(){

}

void x(){
	b();
}
```

### Lvalue References
```cpp
int x = 20;
int& refx = x;

cout << x << "\n"      // prints 20
     << refx++ << "\n" // prints 20 (post-increment)
     << x;             // now x is 21
```
**Output:**
```
20
20
21
```
- References are not objects in C++. A reference is not required to exist or occupy storage. If possible, **the compiler will optimize references away by replacing all occurrences of a reference with the referent.** However, this isn’t always possible, and in such cases, **references may require storage**.

### Arithmetic
#### The Remainder Operator (`operator%`)
- **Naming**: `operator%` is often called the “modulo” or “modulus” operator, this can be confusing, because modulo in mathematics is often defined in a way that yields a different result to what `operator%` in C++ produces when one (and only one) of the operands is negative.
    - For example, in mathematics:
        - -21 modulo 4 = 3
        - -21 remainder 4 = -1
    - For this reason, we believe the name “remainder” is a more accurate name for `operator%` than “modulo”.
- The remainder operator can also work with negative operands. `x % y` always returns results with the sign of _x_.

---

## Best Practices & Tips

- **Initialization**: `int count{15};` uses **brace initialization**, the modern C++11+ style that prevents unsafe type conversions. `int count = 15;` uses **copy initialization**, the older C-style that allows implicit conversions. It is preferable to use `{}` — it’s safer, clearer, and works consistently across all types.
- **Vector Access**: The `.at()` function is often preferred over square brackets `[]` because it lets you know if an error occurs.
- **Function Design**: A function should generally perform one (and only one) task.
- **Reference Definition**: When defining a reference, place the ampersand next to the type (not the reference variable’s name).
- **Remainder Operator Comparison**: Prefer to compare the result of the remainder operator (`operator%`) against 0 if possible.
- **Stream Extraction**: `iss >> word` uses the _stream extraction operator_ (`>>`).
- **The `&` Symbol**: The `&` symbol tends to cause confusion because it has different meanings depending on context:
    - When following a type name, `&` denotes an lvalue reference: `int& ref`.
    - When used in a unary context in an expression, `&` is the address-of operator: `std::cout << &x`.
    - When used in a binary context in an expression, `&` is the Bitwise AND operator: `std::cout << x & y`.

---

## Random Facts & Trivia

- **Loop Variables**: The use of `i`, `j`, and `k` for loop variable names arose because these are the first three shortest names for integral variables in the Fortran programming language. The convention has persisted since.
- **`main` Execution**: A common misconception is that `main` is _always_ the first function that executes. Global variables are initialized prior to the execution of `main`. If the initializer for such a variable invokes a function, then that function will execute prior to `main`.
- **DRY vs WET**: The (snarky) opposite of **[[DRY]]** is **WET** (“Write everything twice”).

---

## References
[Timestamp: 2025/11/17 00:32:13]

**user**: again
[Context: Notes: -2 Resources Summarized/learncpp.com.md]
[Timestamp: 2025/11/17 00:38:24]

**ai**: Of course, here is the reorganized version of your note again.

# learncpp.com

**Source material**: https://www.learncpp.com/
**Tags**: [[C++]], [[programming]]

---

## Core C++ Concepts

### `main()` Function
When the program is executed, the operating system makes a function call to `main()`. Execution then jumps to the top of `main()`. The statements in `main()` are executed sequentially. Finally, `main()` returns an integer value (usually `0`), and your program terminates.

- You should define your `main()` function at the bottom of your code file, below other functions, and avoid calling it explicitly.

### Datatypes
#### Vectors
- Dynamic array (resizable).
- Arrays are just static arrays.

To create a vector, use the `vector` keyword, and specify the type of values it should store within angle brackets `<>` and then the name of the vector, like: `vector <Type> vectorName`.

**Example:**
```cpp
std::vector<type> Cars;
```

### Loop Types
C++ has 3 loop types:
- **for**
- **while**
    - When you put a semicolon (;) after a while loop it's considered bodyless and will loop forever.
        - We can leverage this to our use by making a while loop that calls a function until it's false.
        ```cpp
        while(runUntilFalse);
        ```
    - Be careful about placing a semicolon after the condition of a while-statement, as it will result in an infinite loop unless the condition has some way to evaluate to false.
- **do while**

### Functions
A function within a function is illegal.
```cpp
// Illegal - will not work
void x(){
	void b(){
	} 
}

// Correct way
void b(){

}

void x(){
	b();
}
```

### Lvalue References
```cpp
int x = 20;
int& refx = x;

cout << x << "\n"      // prints 20
     << refx++ << "\n" // prints 20 (post-increment)
     << x;             // now x is 21
```
**Output:**
```
20
20
21
```
- References are not objects in C++. A reference is not required to exist or occupy storage. If possible, **the compiler will optimize references away by replacing all occurrences of a reference with the referent.** However, this isn’t always possible, and in such cases, **references may require storage**.

### Arithmetic
#### The Remainder Operator (`operator%`)
- **Naming**: `operator%` is often called the “modulo” or “modulus” operator, this can be confusing, because modulo in mathematics is often defined in a way that yields a different result to what `operator%` in C++ produces when one (and only one) of the operands is negative.
    - For example, in mathematics:
        - -21 modulo 4 = 3
        - -21 remainder 4 = -1
    - For this reason, we believe the name “remainder” is a more accurate name for `operator%` than “modulo”.
- The remainder operator can also work with negative operands. `x % y` always returns results with the sign of _x_.

---

## Best Practices & Tips

- **Initialization**: `int count{15};` uses **brace initialization**, the modern C++11+ style that prevents unsafe type conversions. `int count = 15;` uses **copy initialization**, the older C-style that allows implicit conversions. It is preferable to use `{}` — it’s safer, clearer, and works consistently across all types.
- **Vector Access**: The `.at()` function is often preferred over square brackets `[]` because it lets you know if an error occurs.
- **Function Design**: A function should generally perform one (and only one) task.
- **Reference Definition**: When defining a reference, place the ampersand next to the type (not the reference variable’s name).
- **Remainder Operator Comparison**: Prefer to compare the result of the remainder operator (`operator%`) against 0 if possible.
- **Stream Extraction**: `iss >> word` uses the _stream extraction operator_ (`>>`).
- **The `&` Symbol**: The `&` symbol tends to cause confusion because it has different meanings depending on context:
    - When following a type name, `&` denotes an lvalue reference: `int& ref`.
    - When used in a unary context in an expression, `&` is the address-of operator: `std::cout << &x`.
    - When used in a binary context in an expression, `&` is the Bitwise AND operator: `std::cout << x & y`.

---

## Random Facts & Trivia

- **Loop Variables**: The use of `i`, `j`, and `k` for loop variable names arose because these are the first three shortest names for integral variables in the Fortran programming language. The convention has persisted since.
- **`main` Execution**: A common misconception is that `main` is _always_ the first function that executes. Global variables are initialized prior to the execution of `main`. If the initializer for such a variable invokes a function, then that function will execute prior to `main`.
- **DRY vs WET**: The (snarky) opposite of **[[DRY]]** is **WET** (“Write everything twice”).
[Timestamp: 2025/11/17 00:38:38]

**user**: again, but edit gramaticall and english mistakes, don't use diffrenet words tho
[Context: Notes: -2 Resources Summarized/learncpp.com.md]
[Timestamp: 2025/11/18 16:48:16]

**ai**: Of course. Here is the reorganized and grammatically corrected version of your note.

# learncpp.com

**Source material**: https://www.learncpp.com/
**Tags**: [[C++]], [[programming]]

---

## Core C++ Concepts

### `main()` Function
When the program is executed, the operating system makes a function call to `main()`. Execution then jumps to the top of `main()`. The statements in `main()` are executed sequentially. Finally, `main()` returns an integer value (usually `0`), and your program terminates.

- You should define your `main()` function at the bottom of your code file, below other functions, and avoid calling it explicitly.

### Datatypes
#### Vectors
- Dynamic array (resizable).
- Arrays are just static arrays.

To create a vector, use the `vector` keyword, and specify the type of values it should store within angle brackets `<>` and then the name of the vector, like: `vector <Type> vectorName`.

**Example:**
```cpp
std::vector<type> Cars;
```

### Loop Types
C++ has 3 loop types:
- **for**
- **while**
    - When you put a semicolon (;) after a while loop, it's considered bodyless and will loop forever.
        - We can leverage this to our use by making a while loop that calls a function until it's false.
        ```cpp
        while(runUntilFalse);
        ```
    - Be careful about placing a semicolon after the condition of a while-statement, as it will result in an infinite loop unless the condition has some way to evaluate to false.
- **do while**

### Functions
A function within a function is illegal.
```cpp
// Illegal - will not work
void x(){
	void b(){
	} 
}

// Correct way
void b(){
}

void x(){
	b();
}
```

### Lvalue References
```cpp
int x = 20;
int& refx = x;

cout << x << "\n"      // prints 20
     << refx++ << "\n" // prints 20 (post-increment)
     << x;             // now x is 21
```
**Output:**
```
20
20
21
```
- References are not objects in C++. A reference is not required to exist or occupy storage. If possible, **the compiler will optimize references away by replacing all occurrences of a reference with the referent.** However, this isn’t always possible, and in such cases, **references may require storage**.

### Arithmetic
#### The Remainder Operator (`operator%`)
- **Naming**: `operator%` is often called the “modulo” or “modulus” operator. This can be confusing because modulo in mathematics is often defined in a way that yields a different result to what `operator%` in C++ produces when one (and only one) of the operands is negative.
    - For example, in mathematics:
        - -21 modulo 4 = 3
        - -21 remainder 4 = -1
    - For this reason, we believe the name “remainder” is a more accurate name for `operator%` than “modulo”.
- The remainder operator can also work with negative operands. `x % y` always returns results with the sign of _x_.

---

## Memory and References

### Pass by Value vs. Pass by Reference
**Pass by reference example:**
```c++
#include <iostream>

void swap(std::string &x, std::string &y){
  std::string temp = x;
  x = y;
  y = temp;
}

int main(){
  std::string wc_winner_2018 = "France";
  std::string wc_winner_2022 = "Argentina";
  
  swap(wc_winner_2018, wc_winner_2022);
  
  std::cout << wc_winner_2022 << "\n" << wc_winner_2018;
} 
```
Notice how this wouldn't work without passing by reference. Without it, the swap parameters would be completely different variables with different memory addresses. The swap function's parameters are destroyed at the end of the function's body (its scope).

### Dynamic Memory
Dynamic memory is used when we don't know what the size will be at compile time. For example, when we want to get grades from a teacher, we don't know how many grades he wants to put in each time, so we can do something like this:
```c++
#include <iostream>

int main(){
  int size{};

  std::cout << "how many grades to put in?: ";
  std::cin >> size;

  char *pGrades = new char[size] ; // allocated on the heap, and is a pointer.

  for(int i = 0; i < size; i++){
    std::cout << "Enter the grade of student " << i+1 << ": " ;
    std::cin >> pGrades[i];
  }

  for(int i = 0; i < size; i++){
    std::cout << pGrades[i];
  }
  
  delete[] pGrades; 
}
```

### Heap vs. Stack
| Feature | Stack | Heap |
| :--- | :--- | :--- |
| **Allocation** | Automatic, at function call | Manual (`new`/`delete`) |
| **Access** | Direct via variable names | Via pointers |
| **Speed** | Fast | Slower |
| **Size** | Limited (usually MBs) | Large, limited by RAM |
| **Lifetime** | Until function exits | Until explicitly deleted or program ends |
| **Structure** | LIFO (Last In, First Out) | Free-form pool |
| **Use Case** | Local variables, function calls | Dynamic arrays, objects |
| **Risk** | Stack overflow with deep recursion or large locals | Memory leaks if not deleted |

---

## Best Practices & Tips

- **Initialization**: `int count{15};` uses **brace initialization**, the modern C++11+ style that prevents unsafe type conversions. `int count = 15;` uses **copy initialization**, the older C-style that allows implicit conversions. It is preferable to use `{}` — it’s safer, clearer, and works consistently across all types.
- **Vector Access**: The `.at()` function is often preferred over square brackets `[]` because it lets you know if an error occurs.
- **Function Design**: A function should generally perform one (and only one) task.
- **Reference Definition**: When defining a reference, place the ampersand next to the type (not the reference variable’s name).
- **Remainder Operator Comparison**: Prefer to compare the result of the remainder operator (`operator%`) against 0 if possible.
- **Stream Extraction**: `iss >> word` uses the _stream extraction operator_ (`>>`).
- **The `&` Symbol**: The `&` symbol tends to cause confusion because it has different meanings depending on context:
    - When following a type name, `&` denotes an lvalue reference: `int& ref`.
    - When used in a unary context in an expression, `&` is the address-of operator: `std::cout << &x`.
    - When used in a binary context in an expression, `&` is the Bitwise AND operator: `std::cout << x & y`.

---

## Quick Snippets

- **User Input**: When taking user input using `std::getline`, use `std::getline(std::cin >> std::ws, VARIABLE);` so that it removes any white-space before user input.
- **Ternary Operator**: A Ternary Operator is another syntax for an if-condition.
	- Syntax: `20 > 10 ? /*do x*/ : /*do y*/;`
- **Random Number**: You can generate a random number in C++ by running:
	```c++
	srand(time(0));
	int randnum = (rand() % HIGHESTNUMBERINRANGE) + 1; // highest number in range would be 6 for a dice, etc.
	```
- **Const Parameters**: If you put `const` before the parameter variable in the function definition, you'll get **read-only parameters**.

---

## Trivia & Fun Facts

- **Loop Variables**: The use of `i`, `j`, and `k` for loop variable names arose because these are the first three shortest names for integral variables in the Fortran programming language. The convention has persisted since.
- **`main` Execution**: A common misconception is that `main` is _always_ the first function that executes. Global variables are initialized prior to the execution of `main`. If the initializer for such a variable invokes a function, then that function will execute prior to `main`.
- **DRY vs WET**: The (snarky) opposite of **[[DRY]]** is **WET** (“Write everything twice”).
[Timestamp: 2025/11/18 16:49:34]