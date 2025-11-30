

2025-11-23 00:57

**Source material** : https://youtu.be/CuWfgiwI73Q?t=1067
**Tags** : 

# LUA


--- 
### Basics

comments with `--`

#### datatypes
`local` means don't make this global
`
just 
```lua
local number = 5
local string = "ahmed"
local single = 'ahmed'
local multiline_literal = [[multi line literal]]
local truth,lie = true,false
local nothing = null
```

#### functions
```lua
local function name(arg)
	print("hello",arg)
end -- notice no curly braces just words

local greet = function(name) -- functions as values!
	-- .. is string concat
	print("Greetings, " .. name .. "!") -- this will print Greetings, name!

local higher_order = function(val)
	return function(another)
		return val + another
	end
end 

local mutlipleinpout(...) -- ... means variable params
	local arguments = {...} -- unpack
	for i,v in ipairs({...}) do 
		print(i,v)
	end
	return unpack(arguments) -- multiple returns 
local add_one = higher_order(1)
print("add_one(2)", add_one(2))
```

```lua

local single_string_param(s)
	return s .. "miaw" end
	
local x = single_string_param("hi")
local y = single_string "hi"

print(x,y)
```

```lua 
local setup = function(opts)
	if opts.default = nil then
		opts.default = 17
	end
	
	print(opts.defaultm opts.other)	
end

setup {default = 12, other = false}	
setup {other = true}	

		
```
#### tables

luas only datastructure
as a map and a list
#### as a list
```lua
local list = {"first",2,false,function() print("Fourth!") end}
print("1", list[1]) -- one indexing LMAO
```

#### as a table 
```lua

local t = {literal_key="string",
			["expresion"] = "WORKS",
			[function() end] = true
		  }
print("",t[function() end]) -- not going to print true, for that this function is diffrent from the one in the table 
```

```lua

local MyTable = {}
function MyTable.something(self,...) end
function MyTable:something(...) end -- equviiant
```
#### loop

for lists
```lua
local name = {"name","name2"}
for index = 1, #name do --# means length of array
	print(index,name[index])
end

for index,value in ipairs(name) do 
	print(index,value)
end
```

for maps
```lua
local miaw = {"cat"="fawzy","dog"="rex"}
for key, value in pairs(miaw) do 
	print(key,value) 
end
```


#### conditionals
```lua
local amihuman = true
if amihuman then
		
	print("welcome human")
else
	print("liar")	
	end
end


	
```

only nil and false are false
everything else is truthy


#### modules

```lua
--foo.lua
local M = {} -- M stands for module
m.cool_function = function() end
return m
```

```lua

--bar.lua
local foo = require('foo')
foo.cool_function()
```

### meta-tables

meta-tables are like python dunder methods

```lua
local vector_mt = {}
vector_mt.__add = function(left,right) -- define an __add metatable
	return setmetatable({
		left[1]	+ right[1]
		left[2] + right[2]
		left[3] + right[3]
	}, vector_mt)
	
local v1 = settimetable({3,1,5},vector_mt)
local v1 = settimetable({4,6,5},vector_mt)
local v3 = v1 + v2 -- you can't ussually do that
print(v3)
```

## **References**:

- 
- 

