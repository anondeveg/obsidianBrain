

logs -> records
metrics ->
traces -> transactions, someway to track from the request initialization through all layers until response.

## logging
recording all important events and errors. like a journal or diary of the backend application.
we get "what is happened"
### levels
 when logging particular events we assign levels for that event.
 - debug(most commond in development)
 - info
 - warn (wrong password, etc. failed because of the user etc.)
 - error (any error)
 - fatal (fatal STOPS the application its a very very serious issue.)
### structured vs unstructured
unstructured -> in development, raw text that looks nice to spot errors and parse fast.
structured ->  in production, json(most probably) so that we can give it to third-party tools that manages the logs.
 


## monitoring
keeps looking at the system and checking the app to make sure everything is correct. 
healthchecks etc.

we get metrics,patterns, and trends

## observability
if we can determine the internal state of the application exteranlly .
we get traces and the idea of observability.

instrumenation is measuring differernt attributes of the function

[[opentelemtry]]
