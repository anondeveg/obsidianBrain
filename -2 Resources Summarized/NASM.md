2025-12-29 05:58

**Source material** : https://cs.lmu.edu/~ray/notes/nasmtutorial/

**Tags** : [[Low Level]] [[programming]] 

# NASM
assembly is the human readable version of machine code

no datatypes all is just binary
the only 2 things are
address VS data

there is 3 sections

`.data`
where we put constants. strings,ints,floats etc

`.bss`
	reserving space in memory for future data
`.text`
`_start`
or 
`_main` 
depending on the linker 
ld uses `_start` while gnu uses `_main`
eax for 32 bits
rax for 64 bits


register:
	hardware implemented variables 
		 a set of transistors that hold data


instructions:

### mov dest ,src
 copies data from a place to another
## movzx dest,src
zeros out the rest of the register
it stands for **z**ero e**x**tend

## movsx dest,src
sign extend


## all of the instructions follow dest,src synatx


# bitwise operations
	they go byte by byte rather they go bit by bit
	
## and

## or

## xor

## test


## arthmetic
## add
 add eax ebx ; stands for eax = eax + ebx

## sub
 same as add

## mul
mov ax,15
mul bx  ; rdx:rax = ras * rbx
because it might be larger than rax so we store it in both rdx and rax

## div
div bx ; rdx = ax:dx / bx
[] brackets are used for derefrencing 
	getting the value in the address
![[Pasted image 20251229060013.png]]

Generally, you put code in a section called `.text` and your constant data in a section called `.data`.

pseudo instructions
## **References**:

- 
- 

