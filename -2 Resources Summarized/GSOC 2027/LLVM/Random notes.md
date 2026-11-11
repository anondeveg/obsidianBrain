---
w:
---

normally  


PTU: partial translation unit.

```c++
  // Add a new PTU.
  ASTContext &C = S.getASTContext();
  C.addTranslationUnitDecl();

```
sema = semantic analysis
for example
```c++
int x = "hello";
```
the parses sees this as perfectly fine parsable code but sema says 
int ← incompatible with ← "hello"

The Sema object is the big Clang component responsible for semantic analysis of the current compilation.


```c++
const FunctionDecl *PatternDecl =
    Function->getTemplateInstantiationPattern();
```
if 
```c++
template<typename T>
int f(T) { return 0; }
```
then
``
Function    = f<int>
PatternDecl = f<T>

whether the definition is reachable


9. THIS is important for your bug
```
if (PatternDecl->isLateTemplateParsed() &&
    !LateTemplateParser) {
```
If the template body was delayed, Clang might not actually have the body yet.

So it puts the function into:

`LateParsedInstantiations`

and returns.

Later, when the late parser is available, this happens:

LateTemplateParser(OpaqueParser, *LPTIter->second);

That's where Clang finally parses the delayed template body.

This is directly relevant to #217073.


PTU IS INITSELF DeclContext

and we have declerations like PUT, varDECL
all are stored in DeclContext


clang/lib/StaticAnalyzer/Checkers/CStringChecker.cpp is a Clang Static Analyzer checker — not part of normal compilation. The static analyzer is a separate path (clang --analyze, or scan-build / clang-tidy's clang-analyzer-*) that does symbolic execution: it walks feasible paths through your code tracking abstract values, and reports bugs like buffer overflows and null derefs without running the program.
"Models" means: when the analyzer hits a call to one of these, CStringChecker teaches it what the function does to program state (how far it reads/writes, what it returns, that the destination is now initialized, that the buffers mustn't overlap), and flags the call when the symbolic state proves a rule is violated.


----

(FLL->isExact()) 
isExact means can i represent exactly or do i need to round it?
