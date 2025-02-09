# Structured Query Language

* CRUD and permissions management
* RDBMS  - Relational Database Management System
  * MS SQL, Oracle, MySql, Access
* **data** is stored in objects - tables.
* **Table** is a collection of related data that consists of rows and columns
* Also, it has **fields** and **records** - rows - A **record** is a horizontal entity in a table.
* A **column** is a vertical entity in a table that contains all information associated with a specific field in a table.
* keywords are not case-sensitive
* semicolon might be needed after every statement

## SQL Comments

* `--` single line
* `/**/` multi-line or part of working line

## SQL commands

```sql
    SELECT - extracts data from a database
    UPDATE - updates data in a database
    DELETE - deletes data from a database
    INSERT INTO - inserts new data into a database
    CREATE DATABASE - creates a new database
    ALTER DATABASE - modifies a database
    CREATE TABLE - creates a new table
    ALTER TABLE - modifies a table
    DROP TABLE - deletes a table
    CREATE INDEX -  creates an index (search key)
    DROP INDEX - deletes an index
```

## SELECT and SELECT DISTINCT

* The SELECT statement is used to select data from a database.
* The data returned is stored in a result table, called the result-set.
* The SELECT DISTINCT statement is used to return only distinct (different) values.

```sql
    SELECT column1, column2, ...
    FROM table_name; 
```

## WHERE

* The WHERE clause is used to filter records.
* It is used in SELECT, UPDATE, DELETE...
* It is used to extract only those records that fulfill a specified condition.

```sql
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition; 
```

* operators in SQL ![img.png](img.png)

### AND OR and NOT

* The `WHERE` clause can be combined with `AND`, `OR`, and `NOT` operators.
* The `AND` and `OR` operators are used to filter records based on more than one condition:
  * The `AND` operator displays a record if all the conditions separated by AND are `TRUE`.
  * The `OR` operator displays a record if any of the conditions separated by OR is `TRUE`
* The `NOT` operator displays a record if the condition(s) is `NOT TRUE`.


```sql
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition1 AND condition2 AND condition3 ...;
    
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition1 OR condition2 OR condition3 ...;
    
     SELECT column1, column2, ...
     FROM table_name
     WHERE NOT condition;
```

## ORDER BY

* The ORDER BY keyword is used to sort the result-set in ascending or descending order.
* The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the `DESC` keyword.

```sql
    SELECT column1, column2, ...
    FROM table_name
    ORDER BY column1, column2, ... ASC|DESC; 
```

## INSERT INTO

* The INSERT INTO statement is used to insert new records in a table
* if no columns are specified then ALL columns must be inserted or error will appear

```sql
    INSERT INTO table_name (column1, column2, column3, ...)
    VALUES (value1, value2, value3, ...); 
    
    //or
    
    INSERT INTO table_name
    VALUES (value1, value2, value3, ...); 
```

## NULL values

* A field with a NULL value is a field with no value.
* to test for NULL we need `IS NULL` or `IS NOT NULL` operators

```sql
    SELECT column_names
    FROM table_name
    WHERE column_name IS NULL; 
```

## UPDATE

* The UPDATE statement is used to modify the existing records in a table.
* If you omit the WHERE clause, ALL records will be updated

```sql
  UPDATE table_name
  SET column1 = value1, column2 = value2, ...
  WHERE condition; 
```

## DELETE

* The DELETE statement is used to delete existing records in a table.

```sql
  DELETE FROM table_name WHERE condition;
```

## SQL Functions

### LIMIT / SELECT TOP

* The SELECT TOP clause is used to specify the number of records to return
* Not all database systems support the `SELECT TOP` clause. MySQL supports the `LIMIT` clause to select a limited number of records, while Oracle uses `FETCH FIRST` n `ROWS ONLY` and `ROWNUM`

```sql 
  //mySQL
  SELECT column_name(s)
  FROM table_name
  WHERE condition
  LIMIT number; 
  
  // Sql server
  SELECT TOP number|percent column_name(s)
  FROM table_name
  WHERE condition;
```

### MIN(), MAX()

* The `MIN()` function returns the smallest value of the selected column.
* The `MAX()` function returns the largest value of the selected column.

```sql
  SELECT MIN(column_name)
  FROM table_name
  WHERE condition;
  
  // max
  SELECT MAX(column_name)
  FROM table_name
  WHERE condition; 
```

### COUNT(), AVG(), SUM()

* The `COUNT()` function returns the number of rows that matches a specified criterion.
* The `AVG()` function returns the average value of a numeric column
* The `SUM()` function returns the total sum of a numeric column.

## LIKE operator

* The `LIKE` operator is used in a WHERE clause to search for a specified pattern in a column.
  * The percent sign (`%`) represents zero, one, or multiple characters
  * The underscore sign (`_`) represents one, single character
  * MS Access uses an asterisk (*) instead of the percent sign (%), and a question mark (?) instead of the underscore (_).
* examples ![img_1.png](img_1.png)

```sql
  SELECT column1, column2, ...
  FROM table_name
  WHERE columnN LIKE pattern;
```

## IN Operator

* The IN operator allows you to specify multiple values in a WHERE clause.
* The IN operator is a shorthand for multiple OR conditions.

```sql
  SELECT column_name(s)
  FROM table_name
  WHERE column_name IN (value1, value2, ...); 
  
  //or
  SELECT column_name(s)
  FROM table_name
  WHERE column_name IN (SELECT STATEMENT); 
```

## BETWEEN operator

* The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates.
* The BETWEEN operator is inclusive: begin and end values are included. 

```sql
  SELECT column_name(s)
  FROM table_name
  WHERE column_name BETWEEN value1 AND value2; 
```

## Aliases

* SQL aliases are used to give a table, or a column in a table, a temporary name.
* Aliases are often used to make column names more readable.
* An alias only exists for the duration of that query.
* An alias is created with the `AS` keyword.
* It requires double quotation marks or square brackets if the alias name contains spaces:

```sql
  SELECT column_name AS alias_name
  FROM table_name;
  
  // contains spaces
  SELECT CustomerName AS Customer, ContactName AS [Contact Person]
  FROM Customers; 
```

## JOINS

* A JOIN clause is used to combine rows from two or more tables, based on a related column between them.
* `INNER JOIN` - Returns records that have matching values in both tables
* `LEFT JOIN` - Returns ALL records from the LEFT and matched records from the right table
* `RIGHT JOIN` - Returns ALL records from the RIGHT and matched records from the left table
* `FULL JOIN` - Returns ALL records when there is a match in either left or right table

* ![img_2.png](img_2.png)

### INNER JOIN

* Select records that have matching values in both tables
* If there are records in joined table that do not have matches in first table these orders will not be shown

```sql
  SELECT column_name(s)
  FROM table1
  INNER JOIN table2
  ON table1.column_name = table2.column_name;
  
  // three table inner join
  SELECT o.OrderID, o.OrderDate, c.CustomerName, s.ShipperName
  FROM ((Orders AS o
  JOIN Customers AS c
  ON o.CustomerID=c.CustomerID)
  JOIN Shippers AS s
  ON o.ShipperID=s.ShipperID)
```

### LEFT JOIN

* The LEFT JOIN keyword returns all records from the left table (table1), and the matching records from the right table (table2). 
* The result is 0 records from the right side, if there is no match.
* The LEFT JOIN keyword returns all records from the left table (Customers), even if there are no matches in the right table (Orders).

```sql
  SELECT column_name(s)
  FROM table1
  LEFT JOIN table2
  ON table1.column_name = table2.column_name;
```

### RIGHT JOIN

* The RIGHT JOIN keyword returns all records from the right table (table2), and the matching records from the left table (table1). 
* The result is 0 records from the left side, if there is no match

```sql
  SELECT column_name(s)
  FROM table1
  RIGHT JOIN table2
  ON table1.column_name = table2.column_name;
```


### FULL JOIN

* The FULL OUTER JOIN keyword returns all records when there is a match in left (table1) or right (table2) table records.
* The FULL OUTER JOIN keyword returns all matching records from both tables whether the other table matches or not. So, if there are rows in "Customers" that do not have matches in "Orders", or if there are rows in "Orders" that do not have matches in "Customers", those rows will be listed as well.

```sql
  SELECT column_name(s)
  FROM table1
  FULL OUTER JOIN table2
  ON table1.column_name = table2.column_name
  WHERE condition; 
```

### SELF JOIN

* A self join is a regular join, but the table is joined with itself.

```sql
  SELECT column_name(s)
  FROM table1 T1, table1 T2
  WHERE condition;
```

### UNION and UNION ALL

* The UNION operator is used to combine the result-set of two or more SELECT statements
  * Every SELECT statement within UNION must have the same number of columns
  * The columns must also have similar data types
  * The columns in every SELECT statement must also be in the same order
* To allow duplicate values use UNION ALL

```sql
  SELECT column_name(s) FROM table1
  UNION
  SELECT column_name(s) FROM table2; 
  
  // example
  SELECT 'Customer' AS Type, ContactName, City, Country
  FROM Customers
  UNION
  SELECT 'Supplier', ContactName, City, Country
  FROM Suppliers; 
```

## GROUP BY

 * The GROUP BY statement groups rows that have the same values into summary rows, like "find the number of customers in each country".
 * The GROUP BY statement is often used with aggregate functions (COUNT(), MAX(), MIN(), SUM(), AVG()) to group the result-set by one or more columns.

```sql
  SELECT column_name(s)
  FROM table_name
  WHERE condition
  GROUP BY column_name(s)
  ORDER BY column_name(s);
```

## HAVING

* The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.

```sql
  SELECT column_name(s)
  FROM table_name
  WHERE condition
  GROUP BY column_name(s)
  HAVING condition
  ORDER BY column_name(s);
```

## EXISTS

* The EXISTS operator is used to test for the existence of any record in a subquery.
* The EXISTS operator returns TRUE if the subquery returns one or more records.

```sql
  SELECT column_name(s)
  FROM table_name
  WHERE EXISTS
  (SELECT column_name FROM table_name WHERE condition);
```