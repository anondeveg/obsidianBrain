---
epoch: 1763710417487
modelKey: "gemini-2.5-pro|google"
topic: "Fixing Markdown Table Syntax"


tags:
  - copilot-conversation
---

**user**: not md syntax

| First name | Last name |
| ---------- | --------- |
| Max        | Planck    |
| Marie      | Curie     |

make it like this and make it work 

do it again knowing this info
[Context: Notes: -2 Resources Summarized/MYSQL.md]
[Timestamp: 2025/11/21 09:33:37]

**ai**: Of course. Here is the markdown syntax for the table you provided, which should render correctly:

```markdown
| First name | Last name |
|------------|-----------|
| Max        | Planck    |
| Marie      | Curie     |
```
[Timestamp: 2025/11/21 09:34:12]

**user**: change the synatx of it in my document so that it renders the table 
[Context: Notes: -2 Resources Summarized/MYSQL.md]
[Timestamp: 2025/11/21 09:34:35]

**ai**: Of course. It seems like the markdown table syntax in your note [[MYSQL]] might not be rendering correctly for you. I've adjusted the syntax for all the tables in the note to ensure they display properly.

Here is the updated content for your note:

```markdown
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
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

### Dropping
`DROP TABLE employees;`

**Output:** The `employees` table is completely deleted.

### Altering

#### Adding
If we want to add a phone number column after the initial creation:
`ALTER TABLE employees ADD phone_number varchar(15);`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | phone_number |
|-------------|------------|-----------|------------|-----------|--------------|
|             |            |           |            |           |              |

#### Renaming
We can also rename the column to 'email' if we decide we want an email column instead:
`ALTER TABLE employees RENAME COLUMN phone_number TO email;`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | email |
|-------------|------------|-----------|------------|-----------|-------|
|             |            |           |            |           |       |

#### Modify
But now the 'email' column has inherited the attributes of the previous 'phone_number' column, as we only changed the name. If we want to change the data type size from `varchar(15)` to `varchar(100)` to more realistically hold an email:
`ALTER TABLE employees MODIFY COLUMN email varchar(100);`

**Output:** The table structure looks the same, but the `email` column's data type is now `VARCHAR(100)`.

#### Modify the placement of the column
We can move the column from its current last position to be after 'last_name':
`ALTER TABLE employees MODIFY email VARCHAR(100) AFTER last_name;`

**Output:**
| employee_id | first_name | last_name | email | hourly_pay | hire_date |
|-------------|------------|-----------|-------|------------|-----------|
|             |            |           |       |            |           |

**NOTICE:** We need to restate the entire column definition (name + type) after the `MODIFY` keyword.

#### Make a column the first/last column
If we want to make it the first column:
`ALTER TABLE employees MODIFY email VARCHAR(100) FIRST;`

**Output:**
| email | employee_id | first_name | last_name | hourly_pay | hire_date |
|-------|-------------|------------|-----------|------------|-----------|
|       |             |            |           |            |           |

If you want to make it the last column, you don't need a keyword like `FIRST` because placing it last is the default action.
`ALTER TABLE employees MODIFY email VARCHAR(100);`

#### Delete a column
To delete a column:
`ALTER TABLE employees DROP COLUMN email`;

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

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
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 25.50      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

### Insert specific fields
If we want to add a new row with only a few fields, leaving the rest blank (NULL), we can by specifying which columns we are providing data for:
`INSERT INTO employees (employee_id,first_name,last_name) VALUES(4,"MOSTAFA","MOHAMMED");`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 25.50      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|
| 4           | MOSTAFA    | MOHAMMED  | NULL       | NULL      |

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
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|
| 4           | MOSTAFA    | MOHAMMED  | NULL       | NULL      |

To delete a row, we can:
`DELETE FROM employees WHERE employee_id=4`

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

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
```
[Timestamp: 2025/11/21 09:35:30]

**user**: make every codeblock mutliline with the sql syntaxing
[Context: Notes: -2 Resources Summarized/MYSQL.md]
[Timestamp: 2025/11/21 09:36:47]

**ai**: Of course. I have updated the note [[MYSQL]] to format all SQL commands into multi-line code blocks with SQL syntax highlighting.

Here is the updated content for your note:

```markdown
**2025**-11-21 06:48

**Source material** : https://www.youtube.com/watch?v=5OdVJbNCSso
**Tags** : [[SQL]] [[Databases]]

# MYSQL

---
### DATABASES

To create a database:
```sql
CREATE DATABASE <DBNAME>;
```

To delete a database:
```sql
DROP DATABASE <DBNAME>;
```

To alter a database, for example, to make it read-only:
```sql
ALTER DATABASE <DBNAME> READ ONLY = 1 ;
```

> **Note:** `READ ONLY` is an attribute.

---
## TABLES

### Creation
To create a table named 'employees', we can run:
```sql
CREATE TABLE TABLENAME (COLUMN_NAME DATATYPE,COLUMN2_NAME DATATYPE);
```

So, we can now do:
```sql
CREATE TABLE employees (employee_id INT,first_name VARCHAR(50),last_name VARCHAR(50),hourly_pay DECIMAL(5,2),hire_date DATE);
```

**Output:** An empty table `employees` is created.
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

### Dropping
```sql
DROP TABLE employees;
```

**Output:** The `employees` table is completely deleted.

### Altering

#### Adding
If we want to add a phone number column after the initial creation:
```sql
ALTER TABLE employees ADD phone_number varchar(15);
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | phone_number |
|-------------|------------|-----------|------------|-----------|--------------|
|             |            |           |            |           |              |

#### Renaming
We can also rename the column to 'email' if we decide we want an email column instead:
```sql
ALTER TABLE employees RENAME COLUMN phone_number TO email;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | email |
|-------------|------------|-----------|------------|-----------|-------|
|             |            |           |            |           |       |

#### Modify
But now the 'email' column has inherited the attributes of the previous 'phone_number' column, as we only changed the name. If we want to change the data type size from `varchar(15)` to `varchar(100)` to more realistically hold an email:
```sql
ALTER TABLE employees MODIFY COLUMN email varchar(100);
```

**Output:** The table structure looks the same, but the `email` column's data type is now `VARCHAR(100)`.

#### Modify the placement of the column
We can move the column from its current last position to be after 'last_name':
```sql
ALTER TABLE employees MODIFY email VARCHAR(100) AFTER last_name;
```

**Output:**
| employee_id | first_name | last_name | email | hourly_pay | hire_date |
|-------------|------------|-----------|-------|------------|-----------|
|             |            |           |       |            |           |

**NOTICE:** We need to restate the entire column definition (name + type) after the `MODIFY` keyword.

#### Make a column the first/last column
If we want to make it the first column:
```sql
ALTER TABLE employees MODIFY email VARCHAR(100) FIRST;
```

**Output:**
| email | employee_id | first_name | last_name | hourly_pay | hire_date |
|-------|-------------|------------|-----------|------------|-----------|
|       |             |            |           |            |           |

If you want to make it the last column, you don't need a keyword like `FIRST` because placing it last is the default action.
```sql
ALTER TABLE employees MODIFY email VARCHAR(100);
```

#### Delete a column
To delete a column:
```sql
ALTER TABLE employees DROP COLUMN email;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

### INSERTION
Now, to populate the table, we can insert values like this:
```sql
INSERT INTO TABLE TABLENAME VALUES(COL1,COL2,COL3,etc);
```

So, to add some employees, we can:
```sql
 INSERT INTO employees VALUES
                          (1,"MOHAMMED","SALAKA", 25.50,"2025-01-01"),
                          (2,"AHMED","ZIAD", 15.0,"2025-01-02"),
                          (3,"KHALED","YOUSSEF",12,"2020-01-04");
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 25.50      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

### Insert specific fields
If we want to add a new row with only a few fields, leaving the rest blank (NULL), we can by specifying which columns we are providing data for:
```sql
INSERT INTO employees (employee_id,first_name,last_name) VALUES(4,"MOSTAFA","MOHAMMED");
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 25.50      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|
| 4           | MOSTAFA    | MOHAMMED  | NULL       | NULL      |

---
### SELECTION

### Get all rows from a table
```sql
SELECT * FROM employees;
```
`*` means ALL, so it reads like '`SELECT` ALL from table `employees`'.

### Get specific columns
```sql
SELECT COLUMNNAME FROM employees;
```
For example:
```sql
SELECT first_name, last_name FROM employees;
```

#### Get all rows where a specific condition is true
For example, if we want to get all employees with an `hourly_pay` that is greater than 10:
```sql
SELECT * FROM employees WHERE hourly_pay > 10;
```

We have comparison operators other than `>` and `<`:
- `!=` (not equal)
- `IS` (equal to, used for NULL)
- `>=` (greater than or equal to)
- `<=` (less than or equal to)
- `NOT`

For example, if we want to get rows where a value is `NULL` (has no value), we can run:
```sql
SELECT * FROM employees WHERE hourly_pay IS NULL;
```

Or to get every employee that has a non-null `hourly_pay`:
```sql
SELECT * FROM employees where hourly_pay IS NOT NULL;
```

---
### Updating/Deleting

To update the hourly pay of an employee, for example, we can:
```sql
UPDATE employees SET hourly_pay = 10.95 WHERE employee_id=1;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|
| 4           | MOSTAFA    | MOHAMMED  | NULL       | NULL      |

To delete a row, we can:
```sql
DELETE FROM employees WHERE employee_id=4;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

**IMPORTANT!** If you don't include a `WHERE` clause, this command will delete ALL rows in the table.

---
### COMMITTING AND ROLLING-BACK

By default, MySQL auto-commits, which means that it saves every change you make. You might not want this behavior. For example, if you run this query by mistake:
```sql
DELETE FROM employees;
```
it will delete all the data in the table with no way to roll back to a previous state.

To change this behavior, run:
```sql
SET AUTOCOMMIT=OFF;
```

To commit (save your changes):
```sql
COMMIT;
```
This will create a save point to which you can roll back if a mistake happens.

Now, if we run `DELETE FROM employees`
```sql
SELECT * FROM employees;
```
As you can see, all the data is deleted. However, we can get back to the latest save point by just running:
```sql
ROLLBACK;
```
```sql
SELECT * FROM employees;
```
It's back!

## **References**:

-
```
[Timestamp: 2025/11/21 09:37:19]

**user**: so when i run you the next time your job is to 

-1 change all codeblocks to sql mutliline
-2 make output tables in md
[Context: Notes: -2 Resources Summarized/MYSQL.md]
[Timestamp: 2025/11/21 09:40:11]

**ai**: Understood. For future requests, I will ensure that:
1. All code blocks are formatted as multi-line SQL code blocks.
2. All output tables are in proper Markdown format.

I will apply these rules to any content I generate or modify for you.
[Timestamp: 2025/11/21 09:40:22]

**user**: {}
-1 change all codeblocks to sql mutliline
-2 make output tables when you feel it would make sense or when you see an empy table 



[Context: Notes: -2 Resources Summarized/MYSQL.md]
[Timestamp: 2025/11/21 09:48:16]

**ai**: Of course. I have updated the content of your note according to your instructions. All code snippets have been converted to multi-line SQL code blocks, and I've added or corrected Markdown tables where it helps to illustrate the output of a command.

Here is the updated content for your note:

```markdown
**2025**-11-21 06:48

**Source material** : https://www.youtube.com/watch?v=5OdVJbNCSso
**Tags** : [[SQL]] [[Databases]]

# MYSQL

---
### DATABASES

To create a database:
```sql
CREATE DATABASE <DBNAME>;
```

To delete a database:
```sql
DROP DATABASE <DBNAME>;
```

To alter a database, for example, to make it read-only:
```sql
ALTER DATABASE <DBNAME> READ ONLY = 1 ;
```

**Note:`READ ONLY` is an attribute.

---
## TABLES

### Creation
To create a table named 'employees', we can run:
```sql
CREATE TABLE TABLENAME (COLUMN_NAME DATATYPE,COLUMN2_NAME DATATYPE);
```

So, we can now do:
```sql
CREATE TABLE employees (employee_id INT,first_name VARCHAR(50),last_name VARCHAR(50),hourly_pay DECIMAL(5,2),hire_date DATE);
```

**Output:** An empty table `employees` is created.
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

### Dropping
```sql
DROP TABLE employees;
```

**Output:** The `employees` table is completely deleted.

### Altering

#### Adding
If we want to add a phone number column after the initial creation:
```sql
ALTER TABLE employees ADD phone_number varchar(15);
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | phone_number |
|-------------|------------|-----------|------------|-----------|--------------|
|             |            |           |            |           |              |

#### Renaming
We can also rename the column to 'email' if we decide we want an email column instead:
```sql
ALTER TABLE employees RENAME COLUMN phone_number TO email;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date | email |
|-------------|------------|-----------|------------|-----------|-------|
|             |            |           |            |           |       |

#### Modify
But now the 'email' column has inherited the attributes of the previous 'phone_number' column, as we only changed the name. If we want to change the data type size from `varchar(15)` to `varchar(100)` to more realistically hold an email:
```sql
ALTER TABLE employees MODIFY COLUMN email varchar(100);
```

**Output:** The table structure looks the same, but the `email` column's data type is now `VARCHAR(100)`.

#### Modify the placement of the column
We can move the column from its current last position to be after 'last_name':
```sql
ALTER TABLE employees MODIFY email VARCHAR(100) AFTER last_name;
```

**Output:**
| employee_id | first_name | last_name | email | hourly_pay | hire_date |
|-------------|------------|-----------|-------|------------|-----------|
|             |            |           |       |            |           |

**NOTICE:** We need to restate the entire column definition (name + type) after the `MODIFY` keyword.

#### Make a column the first/last column
If we want to make it the first column:
```sql
ALTER TABLE employees MODIFY email VARCHAR(100) FIRST;
```

**Output:**
| email | employee_id | first_name | last_name | hourly_pay | hire_date |
|-------|-------------|------------|-----------|------------|-----------|
|       |             |            |           |            |           |

If you want to make it the last column, you don't need a keyword like `FIRST` because placing it last is the default action.
```sql
ALTER TABLE employees MODIFY email VARCHAR(100);
```

#### Delete a column
To delete a column:
```sql
ALTER TABLE employees DROP COLUMN email;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

### INSERTION
Now, to populate the table, we can insert values like this:
```sql
INSERT INTO TABLE TABLENAME VALUES(COL1,COL2,COL3,etc);
```

So, to add some employees, we can:
```sql
 INSERT INTO employees VALUES
                          (1,"MOHAMMED","SALAKA", 25.50,"2025-01-01"),
                          (2,"AHMED","ZIAD", 15.0,"2025-01-02"),
                          (3,"KHALED","YOUSSEF",12,"2020-01-04");
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 25.50      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

### Insert specific fields
If we want to add a new row with only a few fields, leaving the rest blank (NULL), we can by specifying which columns we are providing data for:
```sql
INSERT INTO employees (employee_id,first_name,last_name) VALUES(4,"MOSTAFA","MOHAMMED");
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 25.50      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|
| 4           | MOSTAFA    | MOHAMMED  | NULL       | NULL      |

---
### SELECTION

### Get all rows from a table
```sql
SELECT * FROM employees;
```
`*` means ALL, so it reads like '`SELECT` ALL from table `employees`'.

### Get specific columns
```sql
SELECT COLUMNNAME FROM employees;
```
For example:
```sql
SELECT first_name, last_name FROM employees;
```

#### Get all rows where a specific condition is true
For example, if we want to get all employees with an `hourly_pay` that is greater than 10:
```sql
SELECT * FROM employees WHERE hourly_pay > 10;
```

We have comparison operators other than `>` and `<`:
- `!=` (not equal)
- `IS` (equal to, used for NULL)
- `>=` (greater than or equal to)
- `<=` (less than or equal to)
- `NOT`

For example, if we want to get rows where a value is `NULL` (has no value), we can run:
```sql
SELECT * FROM employees WHERE hourly_pay IS NULL;
```

Or to get every employee that has a non-null `hourly_pay`:
```sql
SELECT * FROM employees where hourly_pay IS NOT NULL;
```

---
### Updating/Deleting

To update the hourly pay of an employee, for example, we can:
```sql
UPDATE employees SET hourly_pay = 10.95 WHERE employee_id=1;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|
| 4           | MOSTAFA    | MOHAMMED  | NULL       | NULL      |

To delete a row, we can:
```sql
DELETE FROM employees WHERE employee_id=4;
```

**Output:**
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

**IMPORTANT!** If you don't include a `WHERE` clause, this command will delete ALL rows in the table.

---
### COMMITTING AND ROLLING-BACK

By default, MySQL auto-commits, which means that it saves every change you make. You might not want this behavior. For example, if you run this query by mistake:
```sql
DELETE FROM employees;
```
it will delete all the data in the table with no way to roll back to a previous state.

To change this behavior, run:
```sql
SET AUTOCOMMIT=OFF;
```

To commit (save your changes):
```sql
COMMIT;
```
This will create a save point to which you can roll back if a mistake happens.

Now, if we run `DELETE FROM employees`
```sql
SELECT * FROM employees;
```

As you can see, all the data is deleted.
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
|             |            |           |            |           |

However, we can get back to the latest save point by just running:
```sql
ROLLBACK;
```
```sql
SELECT * FROM employees;
```
It's back!
| employee_id | first_name | last_name | hourly_pay | hire_date |
|-------------|------------|-----------|------------|-----------|
| 1           | MOHAMMED   | SALAKA    | 10.95      | 2025-01-01|
| 2           | AHMED      | ZIAD      | 15.00      | 2025-01-02|
| 3           | KHALED     | YOUSSEF   | 12.00      | 2020-01-04|

## **References**:

-
```
[Timestamp: 2025/11/21 09:49:00]