follow the standards.


## history

in 1990 tim berners-lee invented the WWW to share information.
in the proccess he invented:

- URI
	- Uniform resource identefier
- HTTP
- HTML
- first web-server
- web browser
- first WYSIWYG

### the problem

the scale of WWW made the need of standards and practices

### the fix
in 1993 roy fielding proposed some techniques and ideas to fix the WWW scalability problem.

- 1 client-server SOCs
- 2 UNIFORM INTERFACE 
	- resource 
	-  
	- 
	- 
- 3 layered system
- 4 cache
- 5 stateless (each request is seperate and has all the information of the request) 
- 6 CODE ON DEMAND 

TODO: 
	read HTTP1.1 specifcation
	read REST paper

REST means:
	- representational:
		objects are represented in specified formats (json,xml,etc)
	 - state
	 - transform

## standards

make resources plural
`/books`

do not put underscores or spaces but
when accessing slugs make it underscore with hyphens
`/books/harry-potter`

IDEMPOTENCY:
	calling the same endpoint no matter how many times the outcome has to stay the same.

HTTP methods:
	5 major methods:
		 GET
		 POST
		 PUT
		 PATCH
		 DELETE
		 
		 
	
