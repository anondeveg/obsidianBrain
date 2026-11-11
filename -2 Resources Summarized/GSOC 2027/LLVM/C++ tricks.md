in clang/Basic/TokenKinds.def
```c++
#ifndef PUNCTUATOR
#define PUNCTUATOR(X,Y) TOK(X)

PUNCTUATOR(lesslessless, "<<<")
```
notice how y isn't even used. it's only for readability and the ability to later make 
```
#define PUNCTUATOR(X,Y) Y
```
and use it somewhere else.