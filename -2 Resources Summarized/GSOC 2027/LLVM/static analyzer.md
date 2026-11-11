job: finds bugs statitcally at compile time without running the code.

analyzes sequence of events not just one line.
mimics normal program execution.
takes all source code information in context.

to watch: building a checker in 24 hours.


algorithms & ds in static analyzer:
AST
Control flow graph (CFG):
	cfg is not used for actual compilation, but for emiting warnings.
	it is the order in which  statements are executed.
    it might also have branches.
	
exploded-graph:
	bugs are simply nodes in the exploded-graph

static analyzer is just a converter from AST -> exploded-graph 
displaying the error to the user too.

# exploded graph

exploded graph is just paths through CFG.

it has nodes which are (point,state) pairs.
edges: if a node(point1,state1) has an edge with (point2,state2) that means that the statement **between** point1 and point2 updates state1 to state2.
## program points
each statment is in betwen 2 program points
and each program point is in between 2 statments.

![[Pasted image 20260901070432.png]]

![[Pasted image 20260901070449.png]]

program points stores execution locations like:
	pre-statment
	post-statement
	entereing a call
and 
an abstract stack-frame

## program state

a record of effects of statements evaluated so far.

## states

we have
Environment:
	a hashmap between: Expr -> values
 store: memory location -> value
  constraints on symbolic events
 generic datamap (GDM):
	 each checker uses GDM to store its internal state.
 
one of the most important states is `store`

state1 = nothing yet
statement:
```c++
int x = 7
```
state2
```
program state:
	STORE: x->7
```

also we have **Environment** Exprs

for example
state2:
`STORE: x->7`
statement:
```c++
x + 5;
```

state3:
```
program state:
	STORE:
		 x->7
	Exprs:
		x + 5 -> 12

```
so it keeps track of all we have computed so far.

#### what if there is no data at store at expr time?
for example
```c++
int foo(int x){
	return x;
}
```

if we are analyzing function foo and we are trying to return x we still don't have any value for it.

so, the analyzer creates a symbolic value for it.
```
program state:
	Exprs:
	  x -> reg_$0<int x>
```
we still don't know what x is, but now we can track it and refer to it.

but think about it, now if we have this:
```c++
if(x > 5){
	do xyz;
}
```
what branch should the static analyzer take with the symbolic value? 
well, because we don't know what x actually is, so we take both ways and keep track of the constraints.
```
program state:
	Ranges:
		reg_$0<int x> > 5	
```
and another branch:
```
program state:
	Ranges:
		reg_$0<int x> <= 5
```

also we have to keep in mind not exploring paths in which constraints contradict each other.


#### path explosion! boom
if we have many if statements, the amount of states might increase exponantialy.



# Buillding a checker in 24h

symbolic execution is like normal execution
but instead of exploring only one path it explores all paths.

it uses symbolic values
it collects constraints on symbolic values
uses these constraints to determine feasable paths.


## checkers
checkers participate in the graph construction.
checkers can stop path exploration by creating sink nodes:
	if it finds a bug it can tell core to stop exploring.


**CHECKERS ARE VISITORS**

![[Pasted image 20260901085257.png]]

checkbind is another name for store.


## a checker recipe

### State
checker state is part of program state.
