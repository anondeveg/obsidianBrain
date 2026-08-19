

q1

https://en.wikipedia.org/wiki/Lexical_grammar
https://www.youtube.com/watch?v=9syvZr-9xwk

a regular language is a language that can be represented using a finite automata.
python and haskell can not be represented as finite automata because

> they have to recognize changes in the indentation level as tokens. Doing that requires comparing the amount of whitespace at the start of consecutive lines, which can't be done using a regular grammar. 
 > - [shponglespore - reddit](https://www.reddit.com/r/compsci/comments/kkzn3r/the_lexical_grammars_of_python_and_haskell_are/) 


q2:
for c 
in C macro definitions white-space matters, eg. `#define print(t) puts(#t);` is not the same as `#define print (t) puts(#t);` all things after the macro name that are spaced are considered as macro body 

q3:
	Our scanner here, like most, discards comments and whitespace since those aren’t needed by the parser. Why might you want to write a scanner that does not discard those? What would it be useful for? 

parsing comments can be used to export documenation from code. 
whitespaces can be used as part of the syntax the python for example treats indentation.