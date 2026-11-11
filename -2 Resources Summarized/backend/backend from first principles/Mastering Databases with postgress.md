
# why?
persistant storage

# what is a database?

any persistant thing that offers CRUD operations on data

# database types

## Persistant databases
relational databases like postgresql,mariadb , etc and non-relational db like mongodb

## Ram database
Redis etc

# DBMS 

responsibilities:
- 1 organization of data
- 2 exposing a CRUD API
- 3  Data Integrity

# types of DBMS
## relational
has tables,rows,columns,
predefined schema
and because of that it offers data-integrity
uses SQL(most probably)

## non-relational
like mongo-db.
no schema, really good when you don't know the schema of the data beforehand.

dosen't have data-integrity so you have to implemenet it yourself at the application level, which is error prone.


## why postgresql
- 1 FOSS
- 2 uses SQL standard
- 3 extensible
- 4 reliable and extensible
- 5 really good json support

because of that it should be the first choice!


## SQL NOTES

if accuraccy is important use decimal

char(x) always stores x charachters, if the input is less then it will pad it.
use varchar or text 
DO NOT USE CHAR UNLESS YOU ABSOLUTELLY KNOW HOW MUCH DATA YOU WILL STORE.

use text instead of varchar when possible.

use jsonb instead of json for performance gains.

make field not-null unless there is a reason it can be nullable

make table names plural, small_case and snail_case

you can use to_jsonb() function to make data into a json column in joins/etc

use `:variable`   to make safe queries .

use triggers for repetitve tasks, like changing last_updated time

Index default parameters (sort desc by creation_date etc etc) to make default search faster.
## db management

TRY TO MAKE DATA-INTEGRITY completely done by the database
use enums etc

### migrations
as backend engineers we don't interact with the database directly,because writing queries in the database is not retrivable nor repetable, so we make migration files. 
Migration files are normal sql queries written in .sql files and the files are sequintel
```
1.sql
2.sql
3.sql
4...
```
then we use tools like go-migrate that applies those migrations.:w

people either write both up and down migrations
or only write up migrations with rolling-back as an up-migraton on top of the previous up-migration


### seeding 
is a migration file that inserts test-data


## Defualts

![[Pasted image 20260824062703.png]]


## Advanced
[[B-Tree]]
