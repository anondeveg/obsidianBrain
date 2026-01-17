2025-12-28 13:16

**Source material** :  https://www.cs.sfu.ca/~ashriram/Courses/CS295/assets/books/CSAPP_2016.pdf


**Tags** : [[Low Level]] [[programming]] [[Hardware]] 

## DIRECT QUOTATION

# tour of computer systems

Aside Origins of the C programming language
C was developed from 1969 to 1973 by Dennis Ritchie of Bell Laboratories. The American National
Standards Institute (ANSI) ratified the ANSI C standard in 1989, and this standardization later became
the responsibility of the International Standards Organization (ISO). The standards define the C
language and a set of library functions known as the C standard library. Kernighan and Ritchie describe
ANSI C in their classic book, which is known affectionately as “K&R” [61]. In Ritchie’s words [92], C
is “quirky, flawed, and an enormous success.” So why the success?
. C was closely tied with the Unix operating system. C was developed from the beginning as the
system programming language for Unix. Most of the Unix kernel (the core part of the operating
system), and all of its supporting tools and libraries, were written in C. As Unix became popular in
universities in the late 1970s and early 1980s, many people were exposed to C and found that they
liked it. Since Unix was written almost entirely in C, it could be easily ported to new machines,
which created an even wider audience for both C and Unix.
. C is a small, simple language.The design was controlled by a single person, rather than a committee,
and the result was a clean, consistent design with little baggage. The K&R book describes the
complete language and standard library, with numerous examples and exercises, in only 261 pages.
The simplicity of C made it relatively easy to learn and to port to different computers.
. C was designed for a practical purpose. C was designed to implement the Unix operating system.
Later, other people found that they could write the programs they wanted, without the language
getting in the way.
C is the language of choice for system-level programming, and there is a huge installed base of
application-level programs as well. However, it is not perfect for all programmers and all situations.
C pointers are a common source of confusion and programming errors. C also lacks explicit support
for useful abstractions such as classes, objects, and exceptions. Newer languages such as C++ and Java
address these issues for application-level programs.


relocatable object
program


Aside The GNU project
Gcc is one of many useful tools developed by the GNU (short for GNU’s Not Unix) project. The
GNU project is a tax-exempt charity started by Richard Stallman in 1984, with the ambitious goal of
developing a complete Unix-like system whose source code is unencumbered by restrictions on how
it can be modified or distributed. The GNU project has developed an environment with all the major
components of a Unix operating system, except for the kernel, which was developed separately by
the Linux project. The GNU environment includes the emacs editor, gcc compiler, gdb debugger,
assembler, linker, utilities for manipulating binaries, and other components. The gcc compiler has
grown to support many different languages, with the ability to generate code for many different
machines. Supported languages include C, C++, Fortran, Java, Pascal, Objective-C, and Ada.
The GNU project is a remarkable achievement, and yet it is often overlooked. The modern open-
source movement (commonly associated with Linux) owes its intellectual origins to the GNU project’s
notion of free software (“free” as in “free speech,” not “free beer”). Further, Linux owes much of its
popularity to the GNU tools, which provide the environment for the Linux kernel.
. Linking phase.Notice that our hello program calls the printf function, which
is part of the standard C library provided by every C compiler. The printf
function resides in a separate precompiled object file called printf.o, which
must somehow be merged with our hello.o program. The linker (ld) handles
this merging. The result is the hello file, which is an executable object file (or
simply executable) that is ready to be loaded into memory and executed by
the system.
1.3 It Pays to Understand How Compilation Systems Work
For simple programs such as hello.c, we can rely on the compilation system to
produce correct and efficient machine code. However, there are some important
reasons why programmers need to understand how compilation systems work:
. Optimizing program performance. Modern compilers are sophisticated tools
that usually produce good code. As programmers, we do not need to know
the inner workings of the compiler in order to write efficient code. However,
in order to make good coding decisions in our C programs, we do need a
basic understanding of machine-level code and how the compiler translates
different C statements into machine code. For example, is a switch statement
always more efficient than a sequence of if-else statements? How much
overhead is incurred by a function call? Is a while loop more efficient than
a for loop? Are pointer references more efficient than array indexes? Why
does our loop run so much faster if we sum into a local variable instead of an
argument that is passed by reference? How can a function run faster when we
simply rearrange the parentheses in an arithmetic expression?In Chapter 3, we introduce x86-64, the machine language of recent gen-
erations of Linux, Macintosh, and Windows computers. We describe how
compilers translate different C constructs into this language. In Chapter 5,
you will learn how to tune the performance of your C programs by making
simple transformations to the C code that help the compiler do its job better.
In Chapter 6, you will learn about the hierarchical nature of the memory sys-
tem, how C compilers store data arrays in memory, and how your C programs
can exploit this knowledge to run more efficiently.

Understanding link-time errors. In our experience, some of the most perplex-
ing programming errors are related to the operation of the linker, especially
when you are trying to build large software systems. For example, what does
it mean when the linker reports that it cannot resolve a reference? What is the
difference between a static variable and a global variable? What happens if
you define two global variables in different C files with the same name? What
is the difference between a static library and a dynamic library? Why does it
matter what order we list libraries on the command line? And scariest of all,
why do some linker-related errors not appear until run time? You will learn
the answers to these kinds of questions in Chapter 7.

Avoiding security holes. For many years, buffer overflow vulnerabilities have
accounted for many of the security holes in network and Internet servers.
These vulnerabilities exist because too few programmers understand the need
to carefully restrict the quantity and forms of data they accept from untrusted
sources. A first step in learning secure programming is to understand the con-
sequences of the way data and control information are stored on the program
stack. We cover the stack discipline and buffer overflow vulnerabilities in
Chapter 3 as part of our study of assembly language. We will also learn about
methods that can be used by the programmer, compiler, and operating system
to reduce the threat of attack.


## buses
Running throughout the system is a collection of electrical conduits called buses
that carry bytes of information back and forth between the components. Buses
are typically designed to transfer fixed-size chunks of bytes known as words. The
number of bytes in a word (the word size) is a fundamental system parameter that
varies across systems. Most machines today have word sizes of either 4 bytes (32
bits) or 8 bytes (64 bits). In this book, we do not assume any fixed definition of
word size. Instead, we will specify what we mean by a “word” in any context that
requires this to be defined

## CPU
The central processing unit (CPU), or simply processor, is the engine that inter-
prets (or executes) instructions stored in main memory. At its core is a word-size
storage device (or register) called the program counter (PC). At any point in time,
the PC points at (contains the address of) some machine-language instruction in
main memory.2
From the time that power is applied to the system until the time that the
power is shut off, a processor repeatedly executes the instruction pointed at by the
program counter and updates the program counter to point to the next instruction.
A processor appears to operate according to a very simple instruction execution
model, defined by its instruction set architecture. In this model, instructions execute
2. PC is also a commonly used acronym for “personal computer.” However, the distinction between
the two should be clear from the context.
in strict sequence, and executing a single instruction involves performing a series
of steps. The processor reads the instruction from memory pointed at by the
program counter (PC), interprets the bits in the instruction, performs some simple
operation dictated by the instruction, and then updates the PC to point to the next
instruction, which may or may not be contiguous in memory to the instruction that
was just executed.
There are only a few of these simple operations, and they revolve around
main memory, the register file, and the arithmetic/logic unit (ALU). The register
file is a small storage device that consists of a collection of word-size registers, each
with its own unique name. The ALU computes new data and address values. Here
are some examples of the simple operations that the CPU might carry out at the
request of an instruction:
. Load: Copy a byte or a word from main memory into a register, overwriting
the previous contents of the register.
. Store: Copy a byte or a word from a register to a location in main memory,
overwriting the previous contents of that location.
. Operate: Copy the contents of two registers to the ALU, perform an arithmetic
operation on the two words, and store the result in a register, overwriting the
previous contents of that register.
. Jump: Extract a word from the instruction itself and copy that word into the
program counter (PC), overwriting the previous value of the PC.
We say that a processor appears to be a simple implementation of its in-
struction set architecture, but in fact modern processors use far more complex
mechanisms to speed up program execution. Thus, we can distinguish the pro-
cessor’s instruction set architecture, describing the effect of each machine-code
instruction, from its microarchitecture, describing how the processor is actually
implemented. When we study machine code in Chapter 3, we will consider the
abstraction provided by the machine’s instruction set architecture. Chapter 4 has
more to say about how processors are actually implemented. Chapter 5 describes
a model of how modern processors work that enables predicting and optimizing
the performance of machine-language programs.

## the journey of a .c file
Given this simple view of a system’s hardware organization and operation, we can
begin to understand what happens when we run our example program. We must
omit a lot of details here that will be filled in later, but for now we will be content
with the big picture.
Initially, the shell program is executing its instructions, waiting for us to type a
command. As we type the characters ./hello at the keyboard, the shell program
reads each one into a register and then stores it in memory, as shown in Figure 1.5.
When we hit the enter key on the keyboard, the shell knows that we have
finished typing the command. The shell then loads the executable hello file by
executing a sequence of instructions that copies the code and data in the hello
Figure 1.5
Reading the hello
command from the
keyboard.
CPU
Register file
PC ALU
Bus interface I/O
bridge
System bus Memory bus
Main
memory
I/O bus
Expansion slots for
other devices such
as network adaptersDisk
controller
Graphics
adapter
DisplayMouse Keyboard
USB
controller
Disk
“hello”
User
types
“hello”
object file from disk to main memory. The data includes the string of characters
hello, world\n that will eventually be printed out.
Using a technique known as direct memory access (DMA, discussed in Chap-
ter 6), the data travel directly from disk to main memory, without passing through
the processor. This step is shown in Figure 1.6.
Once the code and data in the hello object file are loaded into memory,
the processor begins executing the machine-language instructions in the hello
program’s main routine. These instructions copy the bytes in the hello, world\n
string from memory to the register file, and from there to the display device, where
they are displayed on the screen. This step is shown in Figure 1.7.
1.5 Caches Matter
An important lesson from this simple example is that a system spends a lot of
time moving information from one place to another. The machine instructions in
the hello program are originally stored on disk. When the program is loaded,
they are copied to main memory. As the processor runs the program, instruc-
tions are copied from main memory into the processor. Similarly, the data string
hello,world\n, originally on disk, is copied to main memory and then copied
from main memory to the display device. From a programmer’s perspective, much
of this copying is overhead that slows down the “real work” of the program. Thus,
a major goal for system designers is to make these copy operations run as fast as
possible.
Because of physical laws, larger storage devices are slower than smaller stor-
age devices. And faster devices are more expensive to build than their slower
counterparts. For example, the disk drive on a typical system might be 1,000 times
larger than the main memory, but it might take the processor 10,000,000 times
longer to read a word from disk than from memory.
Similarly, a typical register file stores only a few hundred bytes of information,
as opposed to billions of bytes in the main memory. However, the processor can
read data from the register file almost 100 times faster than from memory. Even
more troublesome, as semiconductor technology progresses over the years, this
processor–memory gap continues to increase. It is easier and cheaper to make
processors run faster than it is to make main memory run faster.
To deal with the processor–memory gap, system designers include smaller,
faster storage devices called cache memories (or simply caches) that serve as
temporary staging areas for information that the processor is likely to need in
the near future. Figure 1.8 shows the cache memories in a typical system. An L1
cache on the processor chip holds tens of thousands of bytes and can be accessed
nearly as fast as the register file. A larger L2 cache with hundreds of thousands
to millions of bytes is connected to the processor by a special bus. It might take 5
times longer for the processor to access the L2 cache than the L1 cache, but this is
still 5 to 10 times faster than accessing the main memory. The L1 and L2 caches are
implemented with a hardware technology known as static random access memory
(SRAM). Newer and more powerful systems even have three levels of cache: L1,
L2, and L3. The idea behind caching is that a system can get the effect of both
a very large memory and a very fast one by exploiting locality, the tendency for
programs to access data and code in localized regions. By setting up caches to hold
data that are likely to be accessed often, we can perform most memory operations
using the fast caches.
One of the most important lessons in this book is that application program-
mers who are aware of cache memories can exploit them to improve the perfor-
mance of their programs by an order of magnitude. You will learn more about
these important devices and how to exploit them in Chapter 6.

![[Pasted image 20251228140829.png]]


- listing libraries diffrently to the linker does have an effect


# Tour of Computer Systems - Summary

## C Language History & Success
C was created by Dennis Ritchie at Bell Labs (1969-1973) and standardized by ANSI in 1989. Despite being "quirky and flawed," it succeeded for three reasons:
- **Unix Integration**: C was Unix's system language, making both portable together
- **Simplicity**: Single-designer control created a clean, 261-page specification (K&R book)
- **Practicality**: Designed for real system programming without language overhead

**Limitations**: Confusing pointers, no classes/objects/exceptions (addressed by C++/Java)

## GNU Project
Started by Richard Stallman (1984) to create a free Unix-like system. Developed essential tools (gcc, emacs, gdb, linker) that power modern open-source movement. Linux kernel + GNU tools = modern Linux systems.

## Compilation Pipeline
Source → Preprocessor → Compiler → Assembler → Linker → Executable
- **Linker** merges your code with libraries (e.g., printf.o)
- Library order on command line matters!

## Why Understanding Compilation Matters

### 1. Performance Optimization
Questions to answer:
- Switch vs if-else chains?
- Function call overhead?
- While vs for loops?
- Pointers vs array indexes?
- Local variables vs pass-by-reference?
- Arithmetic expression parentheses ordering?

Understanding machine code helps you write compiler-friendly code.

### 2. Link-Time Errors
Common confusions:
- Unresolved references
- Static vs global variables
- Duplicate global variables across files
- Static vs dynamic libraries
- Library ordering on command line
- Runtime-only linker errors

### 3. Security (Buffer Overflows)
Understanding stack memory layout prevents vulnerabilities from accepting untrusted data.

## Hardware Architecture

### Buses
Electrical conduits carrying data in fixed-size chunks called **words**
- Modern systems: 4 bytes (32-bit) or 8 bytes (64-bit)

### CPU (Central Processing Unit)
**Core component**: Program Counter (PC) register pointing to next instruction

**Execution cycle**:
1. Fetch instruction from memory (at PC address)
2. Interpret instruction bits
3. Execute simple operation
4. Update PC to next instruction

**Basic operations**:
- **Load**: Memory → Register
- **Store**: Register → Memory  
- **Operate**: Register → ALU → Register (arithmetic)
- **Jump**: Update PC (control flow)

**Key distinction**:
- **Instruction Set Architecture (ISA)**: What each instruction does
- **Microarchitecture**: How it's actually implemented (complex optimizations)

## Running a Program: The Journey

1. **Shell waits**: User types `./hello`
2. **Loading**: Shell copies executable from disk → main memory (via DMA)
3. **Execution**: CPU executes instructions from `main()`
4. **Output**: "hello, world\n" copied: Memory → Registers → Display

## Memory Hierarchy & Caching

### The Problem: Processor-Memory Gap
- Disk: 1000× larger than RAM, but 10,000,000× slower
- RAM: Billions of bytes, but 100× slower than registers
- Registers: Few hundred bytes, fastest access
- **Gap widens over time** (processors improve faster than memory)

### The Solution: Cache Memories
Exploit **locality** (programs access nearby data repeatedly)

**Cache levels**:
- **L1**: Tens of KB, nearly register speed
- **L2**: Hundreds of KB to MB, 5× slower than L1, still 5-10× faster than RAM
- **L3**: (Modern systems) Additional level
- **Technology**: SRAM (Static RAM)

**Key insight**: Cache-aware programming can boost performance by **10×** or more

![[Pasted image 20251228140829.png]]

## **References**:

- 
- 

