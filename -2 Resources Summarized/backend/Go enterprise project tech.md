turbo  https://turborepo.dev/docs
Turborepo solves your monorepo's scaling problem. Remote Cache stores the result of all your tasks, meaning that your CI never needs to do the same work twice.

Additionally, task scheduling can be difficult in a monorepo. You may need to build, then test, then lint...

Turborepo schedules your tasks for maximum speed, parallelizing work across all available cores.

bun add -D for dev dependencies

https://github.com/golang-standards/project-layout

/cmd has the main file that starts the server
/internal has all the logic related to the application

have 2 .gitignores one for the project overall 
think debug files etc 
and one for the backend itself
https://github.com/github/gitignore/blob/main/Go.gitignore

[[linting]]

task file `Taskfile.yml` is an alternative to make

config.go
reading from env once
then make it into structs


struct tags is important in refliction which is understanding data at runtime 

trick: start with env variables

[[cors]]

return pointers when 
- 1 the data dosen't need to be copied around (data is too big)
- 2 when you are trying to keep the same data in the whole aplication

init functions in go when you import a package that has an init function 
all init functions will be ran

prefixing env variables is important to not overload system env variablees or other programs env variables

[[unmarshaling]] is just unserialization from json or xml or bytes to langauge obeject

use NewRelic

Distributed tracing is a method used to track, record, and follow the path of a single request as it moves across different services, networks, and databases in a modern software system

database pooling 
is when we open multiple connections to the db instead of creating a new connection each and everytime. making it more effecient

when we are talking about logging it includes 2 aspects
monitroing and observability(we are using new relic)

all different modules should have gracefull shutdown.

LOGGING MONITORING AND OBSERVABILITY IS VERY VERY IMPORTANT
SPECIALLY IN PRODUCTION SYSTEMS.

go context is like a storage that has all the information from the request trhough its life-cycle
so we can share some data between levels.

people either write both up and down migrations
or only write up migrations with rolling-back as an up-migraton on top of the previous up-migration

embed migrations into the executable

create new migrations instead of modifying old ones. because it creates a history of changes.

override is used to override default front-end message with backend one.

[[dependency injection]]

layered backend archeticture