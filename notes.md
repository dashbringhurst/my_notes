This is a repository for my notes.

Okay, here we go:

- Git and Github are two separate things.
- Create a new repository first in Github, then git clone the repository into the codeup-data-science directory ~ (copy SSH from Github and paste after git clone)
- Add, commit, push
- git status to see the status of current files in repository
- Git push every day.
- Git push every day.
- update profile readme periodically. Add cool stuff.
- adding files to .gitignore keeps them from being pushed to Github
- don't nest repositories; keep each repository in its own directory

SQL 7/1/22

CRUD: create, read, update, delete

SQL and MySQL are different...
- RDBMS : software that you run to access the data
- database : actual location on the disk where data exists
- database server : machine holding the data
- database client : program used to connect to and query the database
- DDL : data definition language; commands to change RDBMS or structure of database
- DML : database manipulation language; used to CRUD information from the database (what we will focus on in course)

Access MySQL in command line: mysql -h host_name -u user_name -p

Queries end in semi-colon

SHOW DATABASES; (Command to list databases)
USE database_name; (select a database)
SELECT database(); (Determines what database you currently have selected)
SELECT * FROM table_name; (Pull all from that particular table in current database)
SHOW CREATE DATABASE database_name; (show details of the create process for the database)

Database and schema mean the same thing in MySQL Workbench

Use -- or # to insert a comment of one line
Use /* blah blah blah */ for a multi-line comment

Structure of MySql database:
    - inside the database exists schema (databases)
    - these databases provide the structure for tables

TABLES in MySQL

Each cell of data in a table is exactly that: data
Each piece of datum has an inherent type
That type defines how it can interact and if it can belong in that field
Interchangeable terms in MySql: columns and fields
Tables is sql have some very specific rules about how they are created:
    - Firstly, they must contain a primary key
     - must be unique, cannot be null (null = absence of data), and there can be only one

- Data types:
    
    Numbers
    - INT: integers
    - FLOAT: numbers with decimals
    - DECIMAL (length, precision)
    - BOOLEAN: True / False; 0 = False, 1 = True
        - BOOLEAN is not in sql; TINYINT is used instead
    
    Strings
    - CHAR(length): string with a fixed number of characters
    - VARCHAR(length): strings that can vary up to a maximum number (if you need more than 255 characters, use TEXT instead)
    - TEXT: large block of characters that can be any length

    Dates
    - DATE: a date value without time, typically represented as YYYY-MM-DD
    - TIME: a time down to seconds, using 24H time
    - DATETIME: combined date and time value (time zone not recorded), YYYY-MM-DD HH:MM:SS

Basic Statements

- SELECT is the primary read statement we will be using
    - SELECT (bring me information)
    - _subject_ (field names, computations, etc.)
    - FROM (what table do you want this information from?)
    - _source_ (either with a dot notation or living inside a schema)

    - SELECT * FROM chipotle.orders;
        - select every field from the schema named chipotle and the table named orders inside chipotle
        - better to query the schema with USE instead
    - SELECT _name_ FROM fruits;
        - select a specific field; multiple fields separated by a comma
    - SELECT * FROM _table_ WHERE _field_ = 'name'
        - select all fields from the table where the value in a certain field matches a string
            - syntax: equivalence is denoted by a single =
            - string values exist inside single quotes

- DISTINCT will give us unique values in a field
    - SELECT DISTINCT _column1_, _column2_ FROM _table_;

- Aliasing
    - SELECT 2=2 AS 'equivalency_demo'; (quotes are not needed if there are no spaces)
        - temporarily rename a column, table, or miscellaneous pieces of the query
        - keyword is AS
        
7/5 CLAUSES

Clauses are how we get specifically what we want (usually a gingle field or combination of fields)

- WHERE: give me results specifically under X conditions
- ORDER BY: sort results specfically to my needs
- LIMIT: only give me some of the results back

WHERE comes at the end of a select statement
    - need to specify what we want to narrow down
    - establish equivalency =
    - LIKE, compare string values
    - BETWEEN, inclusive ranges
    - Inequality operators: <, >, <=, =>

- Make sure your order of operations are correct when chaining clauses

ORDER BY
    - DESC: descending
    - ascending is the default choice (ASC)

LIMIT
    - # of rows returned in query

FUNCTIONS
    - Functions in SQL work similarly as they do in other programming languages
    - We can use them as a powerful tool to manipulate the data

- STRING FUNCTIONS
    - Like/Not Like
    - CONCAT(string1, string2, string3, etc...)
        - arguments: comma-separated strings
        - return: single string of concatenated arguments
    - SUBSTR(subject_string, start_index, number of characters)
        - Substring gives a SUBSET of a string, where you specify where you want to start in the string by index, and how long you want it to go
        - arguments: the subject, the starting index, how long you want to go in the substring
    - REPLACE(subject, search, replacement)
        - 
    - UPPER and LOWER()
        - apply uppercase or lowercase
    
- DATE FUNCTIONS
    - NOW()
        - Current date and time
        - Return Format: YYYY-MM-DD HH:MM:SS
    - CURDATE(), CURTIME()
        - Similar, but returns are:
            - CURDATE() -> YYYY-MM-DD
            - CURTIME() -> HH:MM:SS
    - UNIX_TIMESTAMP()
        - 

- CASTING
    - Turn one data type into another
    - When utilizing CAST, we separate the arguments with AS
    - CAST()

- MATH FUNCTIONS
    - AVG()
        - Returns the mean of a numeric dataset
    - MIN()
        - returns the minimum value of a numeric set of data
    - MAX()
        - returns the maximum value of a numeric set of data








SUBQUERIES

- Subquery returning a column, scalar, table:
    1. Write/run the INNER query
    2. Write the OUTER query
    3. Insert the INNER query into the OUTER query

ex. for column
SELECT * FROM customer_subscriptions;
SELECT customer_id FROM customer_subscriptions
WHERE (internet_service_type_id = 3);

(see github for complete query)
 
 ex. for scalar
 1. SELECT avg(total_charges) from customer payments;

 2. select customer_id, monthly_charges, total_charges
 from customer segments
 where total_charges > 2979.82;

 3. select customer_id, monthly_charges, total_charges
 from customer segments
 where total_charges > 
 (SELECT avg(total_charges) from customer payments);

ex. for table
    Find customer_id, average charges, internet service type for all customers
1. select customer_id, avg(monthly_charges) as average_charges
    from customer_payments
    group by customer_id;
2.  select customer_id, internet_service_type_id
    from customer_subscriptions;
    join internet_service_type_id as ist
    on


- When returning a subquery for a table, the subquery must be aliased

CASE STATEMENTS

- Our means of categorizing information
- based on truthful logic

- We will:
    - Create conditions
    - Get a result of said conditions
    - These results will go toward an output

- Let's dive in on chipotle
    
    USE chipotle;

- orders is the only table here (no joins! huzzah!)

    SELECT * FROM orders LIMIT 5;

    SELECT item_name FROM orders WHERE item_name LIKE '%chicken%';

- 'picking out from this list:
- we will grab Chicken Burrito, Chicken Crispy Tacos, and Chicken Soft Tacos
- we will refer to this demographic as chicken tortilla

- basic case statement:
    SELECT item_name,
        CASE item_name
	    WHEN LIKE '%chicken%' THEN 'chickkybowl'
        WHEN 'Chicken Burrito' THEN 'chikkyburrito'
        ELSE 'something else'
    END AS modified_item_name
    FROM orders;

- more verbose method of doing things here:
SELECT COUNT(*),
    CASE 
- rather than specifying the field next to CASE,
- we can specify it on WHEN, so we can apply more flexible logic.
	WHEN item_name IN('Chicken Burrito',
						'Chicken Crispy Tacos',
                        'Chicken Soft Tacos') THEN 'chicken_type_beat'
	ELSE 'something else'
END AS chicken_item_field
- still gotta say from where!
FROM orders
GROUP BY chicken_item_field;

- IF statements:

SELECT 
item_name,
- IF: (truth statement, option 1, option2) etc
IF(item_name = 'Chicken Burrito', True, False) AS is_chick_burr
FROM orders;

TEMP TABLES

    SHOW DATABASES;

- You will only have access to this creation process when in your schema:
- (the one associated with your username)
    USE leavitt_1870;

SHOW TABLES;
- currently not populated

- To create a new table:
- CREATE TEMPORARY TABLE
- followed by what you want to call it 
- followed by whats in it (data types and field names)
CREATE TEMPORARY TABLE my_first_table (
	n INT UNSIGNED NOT NULL);

- it will not show up as a regular table, but...
SHOW TABLES;

- it does exist for us to use now.
SELECT * FROM my_first_table;

- lets throw some values into there:
INSERT INTO my_first_table(n) VALUES (1), (2), (3), (10);

SELECT * FROM my_first_table;

- Insert a new field into the table
- to do this, we need to alter the table structure:
ALTER TABLE my_first_table ADD bonuscol VARCHAR(30);

SELECT * FROM my_first_table;

- let's drop that column out (i've decided I dont like it)
ALTER TABLE my_first_table DROP COLUMN bonuscol;

SELECT * FROM my_first_table;

- SIDE NOTE: creating a table with more than one field
CREATE TEMPORARY TABLE tbl2 (
	col1 INT UNSIGNED NOT NULL,
    col2 VARCHAR(30));
    
SELECT * FROM tbl2;
- Inserting information continues with the syntax from before:
INSERT INTO tbl2(col1,col2) VALUES 
	(3, 'hamsandwich'), 
	(8, 'pizza'), 
    (84, 'happy_friday');

SELECT * FROM tbl2;

- to delete an entire temp table:
DROP TABLE tbl2;
- doesnt exist anymore.
SELECT * FROM tbl2;

- 
CREATE TEMPORARY TABLE chipotle_copy(
SELECT * FROM chipotle.orders);

SELECT * FROM chipotle_copy;

- let's create a new field here:
ALTER TABLE chipotle_copy ADD quant_plus INT;

- sanity check: let's see that it exists
SELECT * FROM chipotle_copy LIMIT 3;
- (yes, and its full of nulls)

UPDATE chipotle_copy SET quant_plus = quantity + 1;

SELECT quantity, quant_plus FROM chipotle_copy;

ALTER TABLE chipotle_copy DROP COLUMN quantity;

SELECT quant_plus FROM chipotle_copy;

