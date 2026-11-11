https://www.youtube.com/watch?v=VqCkCDFLSsc


Ast context
it keeps information around the AST 
identifier table
and source manager
also it has the
entry point to the AST is:
	TranslationUnitDecl* get translation unit decl()

core AST classes:
	Decl for declarations
	Stmt for statments
		expressions are statments
	Type for types

glue classes: are there to get you from one place in the ast to another


glue methods: traversal methods:
	if stmt: IF.getThen() IF.getElse() etc for example
	
	

qualtype: qualifiers on a type, like const.
we have qualtype object that points to its type.
![[Pasted image 20260906094027.png]]


## locations


![[Pasted image 20260906094203.png]]

![[Pasted image 20260906094255.png]]

![[Pasted image 20260906094543.png]]