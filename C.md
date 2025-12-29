2025-12-29 06:50

**Source material** : https://ams148-spring18-01.courses.soe.ucsc.edu/system/files/attachments/section1_0.pdf 

**Tags** :  [[Low Level]]

# C

## basic data types
  
  **int** is the basic 32bit integer
  **char** an 8 bit variable, letters or integers
 
## derived data types
###  array
   basictype[number of enteries]
   ```c
   double[10];
   //double0,...,double10
   ```

###  pointers
```c
#include <stdio.h>

int main(){
	int var = 20;
	int *ip; // just the declaration
	
	ip = &var; // address-of operator

	
	printf("address of var %x\n ", &var);
	printf("pointer %x\n ", ip);
	printf("value of pointer %d\n", *ip);
	
}

```

	
###  structure


# Header Files in C

A header file is a file with the extension .h, and contains C function declarations and macro definitions to be shared between several source files. There are two types of headers: one that the programmer writes and the headers that come with the compiler.

You request to use a header file in your program by including it with the C preprocessing directive #include, like you have seen inclusion of stdio.h header file, which comes along with your compiler.

Including a header file is equal to copying the content of the header file but we do not do it because it will be error-prone and it is not a good idea to copy the content of a header file in the source files, especially if we have multiple source files in a program.

**A simple practice in C or C++ programs is that we keep all the constants, macros, system wide global variables, and function prototypes in the header files and include that header file wherever it is required.**

To use a header we use the compiler directive #include <filename.h> for system header files, and #include "filename.h" for programmer written headers.

If a header file happens to be included twice, the compiler will throw an error. In larger codes this may be challenging. Using the compiler directives can alleviate this error. We use #ifndef within the header file. For example:
```c
# ifndef HEADER_FILE
# define HEADER_FILE
the entire header file file
# endif
```

## **References**:

- 
- 

