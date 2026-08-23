
request life-cycle inside the server

OS -> app -> router -> handler

handler/controller
you get 
2 variables: request and response

handler responsibolities: 
	get params from request (binding)
		if failed return 400 (bad request)
	 validate data
	 transform: (try to make all query parameters optional)
	 make your paramters optional 
	 and assign query parameters etc
	 after getting data from service send the appropriate response with appropriate response code.

service:
    (NO HTTP HTTP HANDLING IS IN THE **HANDLER** )
	 from first glance a service should be just a normal functiojn taht nothing to do with http
	 buisness logic
	 
repository:
	 SOC: take data performs database opration return data
	 every repo does one thing


## middleware
functions in between diffirent jobs

it gets request,response, and next
it can take values and send back a response.
ORDER OF MIDDLEWARED IS IMPORTANT
![[Pasted image 20260823072649.png]]

## request context
state that is scoped for each request.
so that request context is accessible by all middlewares and handlers 
