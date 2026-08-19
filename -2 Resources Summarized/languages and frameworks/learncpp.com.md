---
tags:
  - Resources_Summarized
---

2027-10-18 12:32
# learncpp.com

**Source material**: https://www.learncpp.com/
**Tags**: [[C++]], [[programming]]

---

## Core C++ Concepts

---
### `main()` Function
When the program is executed, the operating system makes a function call to `main()`. Execution then jumps to the top of `main()`. The statements in `main()` are executed sequentially. Finally, `main()` returns an integer value (usually `0`), and your program terminates.

- You should define your `main()` function at the bottom of your code file, below other functions, and avoid calling it explicitly.

---
### Datatypes
#### Vectors
- Dynamic array (resizable).
- Arrays are just static arrays.

To create a vector, use the `vector` keyword, and specify the type of values it should store within angle brackets `<>` and then the name of the vector, like: `vector <Type> vectorName`.

**Example:**
```cpp
std::vector<type> Cars;
```

#### Structs
a structure relates different variables under one name.
for example, a student has a name,age,GPA,and a schoolyear. we can represent this student like this:
```c++
#include <iostream>
struct student{
	std::string name;
	int age;
	double GPA;
	int schoolYear=12; // we can set default values too.
}
int main(){
	student st1;
	st1.name = "Ahmed":
	st1.age = 18;
	st1.GPA = 3.8;
	
	std::cout << st1.name << "\n"<<st1.age<<"\n"<<st1.GPA<<"\n"<<st1.schoolYear;

	}
```

#### passing structs

structs are `pass by value` which means that when you pass the variable `st1` to a function a whole new copy is created for that function; any modifications to the struct members will not reflect on the `st1` variable.

to pass the actual `st1` struct we have to `pass by refrence` using the `adress of operator` `&`like so:
```c++
#include <iostream>
struct student{
	std::string name;
	int age;
	double GPA;
	int schoolYear=12;	
}

void changeShoolYear(student s, int year){
	s.schoolYear = year; // notice how we don't have to return anything 

}
int main(){
	student st1;
	st1.name = "Ahmed":
	st1.age = 18;
	st1.GPA = 3.8;
	
	std::cout st1.schoolYear; // 12
	
	changeSchoolYear(st1,9);
	
	std::cout st1.schoolYear; // 9
	
}
```

### ENUMS	
enums are user defined named integers.
```c++
enum Day = {sunday,monday,tuesday,wednesday,thursday,friday,sturday};
		//    0      1      2       3         4         5      6
		
int main(){
	// can be used with switches
	
	Day today = sunday;
	
	switch(today){
		case **saturday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;
		case **sunday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;
		case **monday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;
		case **tuesday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;
		case **wednesday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;
		case **thursday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;
		case **friday**:
			std::cout << "GREAT ITS THAT DAY (YOU KNOW HOW switches WORK)";
			break;		
	}
}
```
---
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
- **do while (TODO)**



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
        - `-21` modulo 4 = 3
        - `-21` remainder 4 = -1
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
| Feature        | Stack                                              | Heap                                     |
| :------------- | :------------------------------------------------- | :--------------------------------------- |
| **Allocation** | Automatic, at function call                        | Manual (`new`/`delete`)                  |
| **Access**     | Direct via variable names                          | Via pointers                             |
| **Speed**      | Fast                                               | Slower                                   |
| **Size**       | Limited (usually MBs)                              | Large, limited by RAM                    |
| **Lifetime**   | Until function exits                               | Until explicitly deleted or program ends |
| **Structure**  | LIFO (Last In, First Out)                          | Free-form pool                           |
| **Use Case**   | Local variables, function calls                    | Dynamic arrays, objects                  |
| **Risk**       | Stack overflow with deep recursion or large locals | Memory leaks if not deleted              |

---

---
## Function Templates
<small> *functions with multiple types* </small>
imagine that we wanted to create a function that will print the max of 2 elements
we might do with function overloading

```c++
#include <iostream>
int max(int x,int y){
	return (x>y)? x:y ;
}
char max(char x,char y){
	return (x>y)? x:y ;
}
double max(char x, char y){
	return (x>y)? x:y;
}

int main(){
	int x = 2;
	int y = 3;
	cout << max(x,y);
}
```

this would work, but it's unnecessary as we are creating 3 different functions just for one use case. Imagine if we wanted to change how the function works, we would need to change 3 functions, or even more!

to fix this inconvenience in c++ we have **Function Templates** we can instead of typing the literal type name (`int` or `char` etc) we can make a variable that is equal to the input data type. Thinking of this, what do you think a name for this variable would be? The community has decided that a capital `T` is going to be used.

so now rewriting this same code using **Function Templates**:

```c++
template <typename T> // we use this to tell the compiler what T stands for.
T max(T x, T y){
	return (x>y)? x:y;
}

int main(){
	int x = 2;
	int y = 3;
	cout << max(x,y);
}
```

Great! now what if the user wants to know the bigger of 2 different type, for example int vs double?
well now we can tell the compiler we have 2 typenames; lets call the second `U` as it comes after `T` in the alphabet

```c++
template <typename T, typename U> // we use this to tell the compiler what T; U stands for.

	return (x>y)? x:y;
}

int main(){
	int x = 2;
	double y = 3.5;
	cout << max(x,y);
}
```

works right? well not really, now the function returns the `int` `3`  not the `double` `3.5`
to finally fix this we can make the return type auto

```c++
template <typename T, typename U> // we use this to tell the compiler what T; U stands for.
auto max(T x, U y){
	return (x>y)? x:y;
}

int main(){
	int x = 2;
	double y = 3.5;
	cout << max(x,y);
}
```


---


---
### OOP

because of the importance and share-ability of the topic ill make a file just for it. [[Object-Oriented-Programming]]
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