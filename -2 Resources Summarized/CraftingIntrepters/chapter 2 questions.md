# Challenges

1. **Pick an open source implementation of a language you like.**
   - I picked golang.
   - Download the source code and poke around in it: done.
   - Try to find the code that implements the scanner and parser. Are they hand-written, or generated using tools like Lex and Yacc?
     - Hand-written in golang itself (self-hosting).

2. **Just-in-time compilation tends to be the fastest way to implement a dynamically-typed language, but not all of them use it. What reasons are there to not JIT?**
   - 1. It's hard to make secure and often is a big open door for vulnerabilities.
     - [Video to watch later about the topic](https://www.youtube.com/watch?v=45wMEIIPsPA)
   - 2. Requires loading both JITed and original code and functions in memory as well as 2 versions of a lot of things, which requires a whole lot more memory. Trading memory for speed isn't always the right call.
     - [Good source](https://langdev.stackexchange.com/questions/981/what-are-the-advantages-and-disadvantages-of-just-in-time-compilation)

3. **Most Lisp implementations that compile to C also contain an interpreter that lets them execute Lisp code on the fly as well. Why?**
   - To enable interactive development and rapid prototyping.
     - [Good talk about this idea](https://www.youtube.com/watch?v=8Ab3ArE8W3s)