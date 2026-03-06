# MySQL basics

## Databases

- silos of information (data and table)
- databases are separate

[See types of databases](https://www.geeksforgeeks.org/dbms/types-of-databases/).

### Database naming conventions

Yes:

    inventory_management
    customer_records
    sales_analytics

No:

    MyDatabase
    db1
    my database


### Table names conventions

plural nouns (most common):

    users
    orders  
    products
    customers

plural nouns (most common)

    users
    orders
    products
    customers


### Column names

    user_id
    first_name
    created_at
    order_total


### Primary keys
    
    id INT PRIMARY KEY

### Foreign keys

    user_id
    product_id
    order_id

### Join tables (many-to-many)  

    user_roles
    student_courses
    order_products

<br>

Example: shema following conventions

```bash
    CREATE DATABASE ecommerce_store;

    CREATE TABLE users (
        id INT PRIMARY KEY,
        first_name VARCHAR(50),
        last_name VARCHAR(50),
        email VARCHAR(100),
        created_at TIMESTAMP
    );

    CREATE TABLE orders (
        id INT PRIMARY KEY,
        user_id INT,
        order_date DATETIME,
        total_amount DECIMAL(10,2)
    );
```

<br>

## Commands

Run MySQL in Terminal:

    mysql -u root -p

    mysql // Launches the MySQL CLI client program
    -u root // Specifies the username (root) to authenticate as
    -p // Tells MySQL to prompt for a password interactively



See which databases currently exist:
    
    show databases;


Clear screen:

    ctrl L


### Creating database

general (empty, with name)  

    CREATE DATABASE <database_name>;

specific
    
    CREATE DATABASE soap_store;

### Dropping and using database

Dropping (delete)

    DROP DATABASE <database-name>;

Use a database:

    USE <database-name>;

See the database you are in.
Do not add any arguments.

    SELECT database(); 

Shows the database.

<br>

If we now create a new database, to use it, we need to:

    CREATE DATABASE music_store;


    USE music_store;

    // Database changed

    SELECT database();

    // shows the music_store database


<br>

## TABLES

Tables are a collection of data held in a structured format in relational databases.
Databases consist of lots of tables.

**Column**: header of each table

**Rows**: the actual data

1. creating empy table with a structure

2. add data

<br>

### Data types

[See data types documentation](https://dev.mysql.com/doc/refman/8.4/en/data-types.html)

When defining the structure of a table, data types are also defined: **what type of information is permited in each column.**
    
Using now:

    numeric: INT

    - a whole number
    - can be + or - (12, -20)

    string: VARCHAR
    
    - variable-length string 

<br>

CHAR â†’ fixed-size values
VARCHAR â†’ variable-length text (used most of the time)

<br>

| Feature | CHAR | VARCHAR |
|---|---|---|
| Length type | Fixed-length | Variable-length |
| Storage | Always uses the full defined size | Uses only the actual string length |
| Padding | Pads unused space with spaces | No padding |
| Best use case | Data with constant length | Data with varying length |
| Example | `CHAR(2)` for country codes | `VARCHAR(50)` for names |

<br>

```bash
CHAR(10)     â†’ "cat" stored as "cat       "
VARCHAR(10)  â†’ "cat" stored as "cat"
```

<br>

<br>

### Creating tables

MySQL doesn't care about new lines, can be in one line.

    CREATE TABLE <tablename>
    (
        column_name data_type,
        column_name data_type,
    );

<br>

    CREATE TABLE cats
    (
        name varchar(100),
        age INT,
    );

What it shows in Terminal:

    mysql> CREATE TABLE cats (
        -> name VARCHAR(50),
        -> age INT
        -> );
    Query OK, 0 rows affected (0.04 sec)

<br>

Check the created tables:

    SHOW tables;

    // shows the same
    SHOW COLUMNS FROM cats;
    DESC cats;

<br>

### Dropping a table

To drop a table:

    DROP TABLE <table-name>;

To specifically drop the `cats` table:

    DROP TABLE cats;