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
        




