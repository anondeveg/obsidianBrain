# Clang Compiler Frontend (for True Epub)
##### Lee Zhi Eng

## 2.2 Getting started with compilers
### Page 61 @ 30 August 2026 12:01:54 AM
*The knowledge obtained by studying compilers can be used to design other scalable software systems as well.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/p[1]/text()[1].189>)
## 2.2.1 Exploring the compiler workflow
### Page 63 @ 30 August 2026 12:05:33 AM
*The stages of compilation can be described as follows:
Frontend: The frontend does lexical analysis and parsing, which includes both syntax analysis and semantic analysis. The syntax analysis assumes that your program is well-organized according to the language grammar rules. The semantic analysis performs checks on the program’s meaning and rejects invalid programs, such as those that use wrong types.
Middle-end: The middle-end performs various optimizations on the intermediate representation (IR) code (LLVM-IR for Clang).
Backend: The Backend of a compiler takes the optimized or transformed IR and generates machine code or assembly code that can be executed by the target platform.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[1]/p[5]/text()[3].2>)
### Page 63 @ 30 August 2026 12:06:03 AM
*The source program is transformed into different forms as it passes through the various stages. For example, the frontend produces IR code, which is then optimized by the middle-end, and finally converted into native code by the backend (see*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[1]/p[6]/text()[1].0>)
## 2.2.2 Frontend
### Page 65 @ 30 August 2026 12:07:39 AM
*Figure 2.4: Compiler frontend*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/p[2]/span/strong/text().0>)
### Page 67 @ 30 August 2026 01:02:09 AM
*The primary output produced by the Parser is called an abstract syntax tree (AST).*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/p[1]/text()[3].2>)
### Page 68 @ 30 August 2026 01:03:59 AM
*The compound statement consists of other statements, such as return and if .*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/p[2]/text()[7].80>)
### Page 69 @ 30 August 2026 01:04:53 AM
*The Parser performs two activities:
Syntax analysis: the Parser constructs the AST by analyzing the syntax of the program.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/p[3]/text()[1].0>)
### Page 69 @ 30 August 2026 01:05:01 AM
*Semantic analysis: the Parser analyzes the program semantically.
One of the jobs*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/ol/li[2]/div/p/text()[1].0>)
### Page 69 @ 30 August 2026 01:05:16 AM
*semantically.
One of the jobs of the parser is to produce an error message if the parsing fails in either of the syntax or semantic analysis phases.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/ol/li[2]/div/p/text()[4].8>)
### Page 71 @ 30 August 2026 01:07:01 AM
*AST is mainly constructed as a result of syntax analysis, but for certain languages, such as C++, semantic analysis is also crucial for constructing the AST, particularly for C++ template instantiation.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/p[17]/text().0>)
### Page 71 @ 30 August 2026 01:08:06 AM
*Semantic analysis, on the other hand, involves the compiler performing template instantiation, which generates the AST for specific instances of the template. It’s worth noting that the semantic analysis of templates can be quite complex, as the compiler must perform tasks such as type checking, name resolution, and more for each template instantiation. Additionally, the instantiation process can be recursive and lead to a significant amount of code duplication, known as code bloat. To combat this, C++ compilers employ techniques such as template instantiation caching to minimize the amount of redundant code generated.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[2]/p[19]/text()[1].0>)
### Page 72 @ 30 August 2026 01:10:26 AM
*The use of IRs in compilers is a concept that has been around for several decades. The idea of using an intermediate representation to represent the source code of a program during compilation has evolved over time, and the exact date when IR was first introduced in compilers is not clear.
However, it is known that the first compilers in the 1950s and 1960s did not use IRs and instead translated source code directly into machine code. By the 1960s and 1970s, researchers had begun experimenting with using IRs in compilers to improve the efficiency and flexibility of the compilation process.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[3]/p[2]/text().0>)
### Page 72 @ 30 August 2026 01:11:10 AM
*One of the first widely used IRs was three-address code, which was used in the mid-1960s in IBM/360’s FORTRAN compiler. Other early examples of IRs include the register transfer language (RTL) and the static single assignment (SSA) form, which were introduced in the 1970s and 1980s respectively.
Today, the use of IRs in compilers is a standard practice, and many compilers use multiple IRs throughout the compilation process. This allows for more powerful optimization and code generation techniques to be applied.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[2]/section[2]/section[3]/p[4]/text()[1].0>)
## 2.3 Clang driver overview
### Page 73 @ 30 August 2026 01:11:58 AM
*program that controls the compilation process is known as the driver. The driver coordinates different stages of compilation and connects them together*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[3]/p[1]/text()[3].20>)
### Page 73 @ 30 August 2026 01:12:36 AM
*To use Clang as the compiler frontend only, the special option -cc1 must be passed to it.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[3]/p[2]/text()[1].326>)
## 2.3.2 Compilation phases
### Page 74 @ 30 August 2026 01:14:09 AM
*We used two inputs for our example program. The first one is our source code and the second one is a shared library for the standard C++ library. The Clang driver should combine the inputs together, pass them via different phases of the compilation process, and finally, provide the executable file on the target platform.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[3]/section[2]/p[1]/text()[1].0>)
## 2.3.3 Tool execution
### Page 76 @ 30 August 2026 01:17:09 AM
*The phases are combined into several tool executions. The Clang driver invokes different programs to produce the final executable. Specifically, for our example, it calls the clang compiler and the ld linker. Both programs require additional arguments that are set up by the driver.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[3]/section[3]/p[1]/text()[1].0>)
## 2.3.5 Debugging Clang
### Page 84 @ 30 August 2026 01:26:43 AM
*It’s worth mentioning a certain optimization implemented in Clang in 2019 [22]. When using the -c option, the Clang driver doesn’t spawn a new process for the compiler:
$ <...>/llvm-project/install/bin/clang -c hello.cpp  \
                                       -o /tmp/hello.o \
                                       -###
clang version 18.1.0rc ...
InstalledDir: <...>/llvm-project/install/bin
 (in-process)
 "<...>/llvm-project/install/bin/clang-18" "-cc1"..."hello.cpp"
 ...
As shown above, the Clang driver does not spawn a new process and instead calls the ”cc1” tool within the same process. This feature not only improves the compiler’s performance but can also be leveraged for Clang debugging.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[3]/section[5]/p[14]/text()[1].0>)
## 2.4 Clang frontend overview
### Page 90 @ 30 August 2026 01:28:22 AM
*Clang’s frontend part diverges significantly from a typical compiler frontend. The primary reason for this distinction is the complexity of the C++ language. Some features, such as macros, can modify the source code itself, while others, such as typedef, can influence the kind of token.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/p[1]/text()[3].12>)
### Page 91 @ 30 August 2026 01:29:48 AM
*You may notice that, in the preceding command, we utilized the -fsyntax-only option, instructing Clang to only execute the preprocessor, parser, and semantic analysis stages.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/p[3]/text()[1].0>)
## 2.4.1 Frontend action
### Page 91 @ 30 August 2026 01:30:31 AM
*The Clang frontend is capable of executing only one frontend action at a time. A frontend action is a specific task or process that the frontend performs based on the provided compiler option. The following is a list of some possible frontend actions (the table only includes a subset of the available frontend actions):
FrontendAction
Compiler option
Description
EmitObjAction
-emit-obj (default)
Compile to an object file
EmitBCAction
-emit-llvm-bc
Compile to LLVM bytecode
EmitLLVMAction
-emit-llvm
Compile to LLVM readable form
ASTPrintAction
-ast-print
Build ASTs and then pretty-print them.
HTMLPrintAction
-emit-html
Prints the program source in HTML form*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[1]/p[1]/text()[1].0>)
### Page 92 @ 30 August 2026 01:31:43 AM
*One significant change is the naming of the lexer. In Clang, the lexer is referred to as the preprocessor. This naming convention reflects the fact that the lexer implementation is encapsulated within the Preprocessor class.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[1]/p[3]/text()[1].0>)
### Page 93 @ 30 August 2026 01:32:23 AM
*While conventional compilers typically perform both syntax and semantic analysis within the parser, Clang distributes these tasks across different components. The Parser component focuses solely on syntax analysis, while the Sema component handles semantic analysis.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[1]/p[4]/text()[1].63>)
## 2.4.2 Preprocessor
### Page 95 @ 30 August 2026 01:34:27 AM
*of token called annotation tokens. The primary difference is that these tokens also store additional semantic information. For instance, a sequence of normal tokens can be replaced by the parser with a single annotation token that contains information about the type or C++ scope. The primary reason for using such tokens is performance, as it allows for the prevention of reparsing when the parser needs to backtrack.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[2]/p[6]/text()[3].16>)
### Page 98 @ 30 August 2026 01:35:52 AM
*we can see, Clang consumes an annotation token from Line 4 of the program shown in Figure 2.31. The token is located between columns 1 and 7. See Figure 2.32. This corresponds to the following text used as the token: clangbook::A<int>. The token consists of other tokens, such as ’clangbook’, ’::’, and so on. Combining all the tokens into one will significantly simplify the parsing and boost the overall parsing performance*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[2]/p[13]/text()[1].2>)
### Page 98 @ 30 August 2026 01:37:16 AM
*The Lexer class is used to convert a text buffer into a stream of tokens.
The TokenLexer class is used to retrieve tokens from macro expansions.
It should be noted that only one of these helpers can be active at a time.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[2]/ul/li[1]/p/text()[1].0>)
### Page 99 @ 30 August 2026 01:38:03 AM
*depending on whether there is a macro expansion within it. As a result, the Preprocessor class keeps a stack of lexers (IncludeMacroStack class) for each #include directive, as shown in Figure 2.33.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[2]/p[16]/text()[4].2>)
## 2.4.3 Parser and sema
### Page 101 @ 30 August 2026 01:39:39 AM
*Clang utilizes a hand-written recursive-descent parser [10]. This parser can be considered simple, and this simplicity was one key reason for its selection. Additionally, the complex rules specified for the C/C++ languages necessitated an ad hoc parser with easily adaptable rules.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[3]/p[5]/text()[1].0>)
### Page 101 @ 30 August 2026 01:40:32 AM
*source file together with all the headers (16.5.1.2) and source files included (15.3) via the preprocessing directive #include, less any source lines skipped by any of the conditional inclusion (15.2) preprocessing directives, is called a translation unit.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[3]/p[7]/text().1>)
### Page 107 @ 30 August 2026 01:45:02 AM
*The parsing results in the generation of AST. We can also inspect the process of AST creation using the debugger. To do this, we need to set a corresponding breakpoint at the clang::ReturnStmt::Create method:*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[4]/section[3]/p[42]/text()[1].0>)
## 2.5 Summary
### Page 112 @ 30 August 2026 01:48:37 AM
*In this chapter, we have acquired a basic understanding of compiler architecture and delved into the various stages of the compilation process, with a focus on the Clang driver. We have explored the internals of the Clang frontend, studying the Preprocessor that transforms a program into a set of tokens, and the Parser, which interacts with a component called ’Sema’. Together, these elements perform syntax and semantic analysis.
The upcoming chapter will center on the Clang Abstract Syntax Tree (AST)—the primary data structure employed in various Clang tools. We will discuss its construction and the methods for traversing it.*

[View in book](<file:///mnt/onboard/books/low-level/Clang Compiler Frontend_ Understand internals of a top-rated -- Ivan Murashko -- PS, 2024 -- Packt Publishing - ebooks Account -- isbn13 9781837630981 -- e90ddd8f9fc0a770bd7c1bc7975c8d68 -- Anna’s Archive.epub?pos=/body/DocFragment[8]/body/div/div/section/section[5]/p[1]/text().0>)
## 
_Generated at: 2026-08-30-03-40-55_