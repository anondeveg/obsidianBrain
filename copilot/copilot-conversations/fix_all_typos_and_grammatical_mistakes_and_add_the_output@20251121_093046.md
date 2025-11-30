---
epoch: 1763710246999
modelKey: "gemini-2.5-pro|google"
topic: "MySQL Command and Output Correction"


tags:
  - copilot-conversation
---

**user**: fix all typos and grammatical mistakes 
and add the output of each mysql command that changes the table

without changing my commands or explenation  
[Context: Notes: -2 Resources Summarized/MYSQL.md]
[Timestamp: 2025/11/21 09:30:46]

**ai**: Of course! I've corrected the typos and grammatical errors in your note and added the resulting table state after each command that modifies the data or structure.

**2025**-11-21 06:48

**Source material** : https://www.youtube.com/watch?v=5OdVJbNCSso
**Tags** : [[SQL]] [[Databases]]

# MYSQL

---
### DATABASES

To create a database:
`CREATE DATABASE <DBNAME>;`

To delete a database:
`DROP DATABASE <DBNAME>;`

To alter a database, for example, to make it read-only:
`ALTER DATABASE <DBNAME> READ ONLY = 1 ;`

> **Note:** `READ ONLY` is an attribute.

---
## TABLES

### Creation
To create a table named 'employees', we can run:
`CREATE TABLE TABLENAME (COLUMN_NAME DATATYPE,COLUMN2_NAME DATATYPE);`

So, we can now do:
`CREATE TABLE employees (employee_id INT,first_name VARCHAR(50),last_name VARCHAR(50),hourly_pay DECIMAL(5,2),hire_date DATE);`

**Output:** An empty table `employees` is created.
| employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|
| | | | | |

### Dropping
`DROP TABLE employees;`

**Output:** The `employees` table is completely deleted.

### Altering

#### Adding
If we want to add a phone number column after the initial creation:
`ALTER TABLE employees ADD phone_number varchar(15);`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | phone_number |
|---|---|---|---|---|---|
| | | | | | |

#### Renaming
We can also rename the column to 'email' if we decide we want an email column instead:
`ALTER TABLE employees RENAME COLUMN phone_number TO email;`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | email |
|---|---|---|---|---|---|
| | | | | | |

#### Modify
But now the 'email' column has inherited the attributes of the previous 'phone_number' column, as we only changed the name. If we want to change the data type size from `varchar(15)` to `varchar(100)` to more realistically hold an email:
`ALTER TABLE employees MODIFY COLUMN email varchar(100);`

**Output:** The table structure looks the same, but the `email` column's data type is now `VARCHAR(100)`.

#### Modify the placement of the column
We can move the column from its current last position to be after 'last_name':
`ALTER TABLE employees MODIFY email VARCHAR(100) AFTER last_name;`

**Output:**
| employee_id | first_name | last_name | email | hourly_pay | hire_date |
|---|---|---|---|---|---|
| | | | | | |

**NOTICE:** We need to restate the entire column definition (name + type) after the `MODIFY` keyword.

#### Make a column the first/last column
If we want to make it the first column:
`ALTER TABLE employees MODIFY email VARCHAR(100) FIRST;`

**Output:**
| email | employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|---|
| | | | | | |

If you want to make it the last column, you don't need a keyword like `FIRST` because placing it last is the default action.
`ALTER TABLE employees MODIFY email VARCHAR(100);`

#### Delete a column
To delete a column:
`ALTER TABLE employees DROP COLUMN email`;

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|
| | | | | |

### INSERTION
Now, to populate the table, we can insert values like this:
`INSERT INTO TABLE TABLENAME VALUES(COL1,COL2,COL3,etc)`

So, to add some employees, we can:
```sql
 INSERT INTO employees VALUES
                          (1,"MOHAMMED","SALAKA", 25.50,"2025-01-01"),
                          (2,"AHMED","ZIAD", 15.0,"2025-01-02"),
                          (3,"KHALED","YOUSSEF",12,"2020-01-04");
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|
| 1 | MOHAMMED | SALAKA | 25.50 | 2025-01-01 |
| 2 | AHMED | ZIAD | 15.00 | 2025-01-02 |
| 3 | KHALED | YOUSSEF | 12.00 | 2020-01-04 |

### Insert specific fields
If we want to add a new row with only a few fields, leaving the rest blank (NULL), we can by specifying which columns we are providing data for:
`INSERT INTO employees (employee_id,first_name,last_name) VALUES(4,"MOSTAFA","MOHAMMED");`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|
| 1 | MOHAMMED | SALAKA | 25.50 | 2025-01-01 |
| 2 | AHMED | ZIAD | 15.00 | 2025-01-02 |
| 3 | KHALED | YOUSSEF | 12.00 | 2020-01-04 |
| 4 | MOSTAFA | MOHAMMED | NULL | NULL |

---
### SELECTION

### Get all rows from a table
`SELECT * FROM employees;`
`*` means ALL, so it reads like '`SELECT` ALL from table `employees`'.

### Get specific columns
`SELECT COLUMNNAME FROM employees;`
For example:
`SELECT first_name, last_name FROM employees;`

#### Get all rows where a specific condition is true
For example, if we want to get all employees with an `hourly_pay` that is greater than 10:
`SELECT * FROM employees WHERE hourly_pay > 10;`

We have comparison operators other than `>` and `<`:
- `!=` (not equal)
- `IS` (equal to, used for NULL)
- `>=` (greater than or equal to)
- `<=` (less than or equal to)
- `NOT`

For example, if we want to get rows where a value is `NULL` (has no value), we can run:
`SELECT * FROM employees WHERE hourly_pay IS NULL;`

Or to get every employee that has a non-null `hourly_pay`:
`SELECT * FROM employees where hourly_pay IS NOT NULL;`

---
### Updating/Deleting

To update the hourly pay of an employee, for example, we can:
`UPDATE employees SET hourly_pay = 10.95 WHERE employee_id=1`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|
| 1 | MOHAMMED | SALAKA | 10.95 | 2025-01-01 |
| 2 | AHMED | ZIAD | 15.00 | 2025-01-02 |
| 3 | KHALED | YOUSSEF | 12.00 | 2020-01-04 |
| 4 | MOSTAFA | MOHAMMED | NULL | NULL |

To delete a row, we can:
`DELETE FROM employees WHERE employee_id=4`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|---|---|---|---|---|
| 1 | MOHAMMED | SALAKA | 10.95 | 2025-01-01 |
| 2 | AHMED | ZIAD | 15.00 | 2025-01-02 |
| 3 | KHALED | YOUSSEF | 12.00 | 2020-01-04 |

**IMPORTANT!** If you don't include a `WHERE` clause, this command will delete ALL rows in the table.

---
### COMMITTING AND ROLLING-BACK

By default, MySQL auto-commits, which means that it saves every change you make. You might not want this behavior. For example, if you run this query by mistake:
`DELETE FROM employees`
it will delete all the data in the table with no way to roll back to a previous state.

To change this behavior, run:
`SET AUTOCOMMIT=OFF;`

To commit (save your changes):
`COMMIT;`
This will create a save point to which you can roll back if a mistake happens.

Now, if we run `DELETE FROM employees`
`SELECT * FROM employees;`
As you can see, all the data is deleted. However, we can get back to the latest save point by just running:
`ROLLBACK;`
`SELECT * FROM employees;`
It's back!

## **References**:

-
[Timestamp: 2025/11/21 09:31:32]