# MySQL basics

## Databases

[See types of databases](https://www.geeksforgeeks.org/dbms/types-of-databases/).

## Basic comands

```sql
-- comment

-- CTRL + L to clear terminal

CREATE DATABASE <database>;   -- Creates a new database

SHOW DATABASES;                -- Lists all databases available on the MySQL server

USE <database>;               -- Sets specific database as the active database for the session

SELECT DATABASE();             -- Displays the name of the currently selected database

DROP DATABASE database;   -- Permanently deletes the specified database and all its tables
```

<br>

```sql

CREATE TABLE cats (
    cat_id INT AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    PRIMARY KEY (cat_id)
);

SHOW TABLES;                 -- Lists all tables in the currently selected database

SHOW COLUMNS FROM <table>;   -- Displays the column names, types, and attributes of the specified table

DESC <table>;                -- Shows the structure of the table (shortcut for SHOW COLUMNS)

SELECT * FROM <table>;       -- Retrieves all rows and columns from the specified table

DROP TABLE <table>;          -- Permanently deletes the specified table and all its data
```


<br>

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

```sql
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

### Quotations

Good practice to use `'single quotes'` for text because `"double quotes"` give errors in some SQL variants.

Use **escaping** for quote inside a quote.

        INSERT INTO shop(name) VALUES ('Mario\'s pizza');

This will pass:

        INSERT INTO shop(name) VALUES ('She said "haha"');
<br>

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

CHAR       fixed-size values
VARCHAR    variable-length text (used most of the time)

<br>

| Feature | CHAR | VARCHAR |
|---|---|---|
| Length type | Fixed-length | Variable-length |
| Storage | Always uses the full defined size | Uses only the actual string length |
| Padding | Pads unused space with spaces | No padding |
| Best use case | Data with constant length | Data with varying length |
| Example | `CHAR(2)` for country codes | `VARCHAR(50)` for names |

<br>

```sql
CHAR(10)     â†’ "cat" stored as "cat       "
VARCHAR(10)  â†’ "cat" stored as "cat"
```

<br>

<br>

### Creating tables

MySQL doesn't care about new lines, can be in one line.

```sql
    CREATE TABLE <tablename>
    (
        column_name data_type,
        column_name data_type,
    );
```

```sql
    CREATE TABLE cats
    (
        name varchar(100),
        age INT,
    );
```

What it shows in Terminal:

```sql
    mysql> CREATE TABLE cats (
        -> name VARCHAR(50),
        -> age INT
        -> );
    Query OK, 0 rows affected (0.04 sec)
```

<br>

Check the created tables:

```sql
    SHOW tables;

    // shows the same
    SHOW COLUMNS FROM cats;
    DESC cats;
```

<br>

### Dropping a table

To drop a table:

    DROP TABLE <table-name>;

To specifically drop the `cats` table:

    DROP TABLE cats;

<br>

## INSERTING DATA

Re-create the `cats` table:

```sql
CREATE TABLE cats (
    name VARCHAR(50),
    age INT
);
```

### Insert

Insert a cat in one line or in various lines.
**The order matters** when you state which values you will add.

```sql
INSERT INTO cats (name, age) VALUES ('Blue Steele', 5);

INSERT INTO cats (name, age) 
VALUES           ('Jenkins',
                 7);
```

### Multi-inserts

```sql
INSERT INTO cats (name, age) 
VALUES 
  ('Meatball', 5), 
  ('Turkey', 1), 
  ('Potato Face', 15);
```

<br>

### Select

See if the inserted values are in the table.
`*` shows everything in the table.

```sql
SELECT * FROM cats;
```

### Using NOT NULL

```
DESC cats;

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(50) | YES  |     | NULL    |       |
| age   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
```


- `NULL: yes` in the table means `null` is permited.
- in SQL `null` means _no value_ / no information

```
INSERT INTO cats (name) VALUES ('Bingo');

+--------+------+
| name   | age  |
+--------+------+
| Damien |    5 |
| Bach   |    1 |
| Timmy  |   10 |
| Julia  |    3 |
| Honey  |    6 |
| Bingo  | NULL | a valid row with no info about the cat's age
+--------+------+
```

<br>

```
INSERT INTO cats() VALUES();

+--------+------+
| name   | age  |
+--------+------+
| Damien |    5 |
| Bach   |    1 |
| Timmy  |   10 |
| Julia  |    3 |
| Honey  |    6 |
| Bingo  | NULL | valid row
| NULL   | NULL | valid row, but we don't want to do this
+--------+------+
```
<br>

To prevent from being able to not enter the information, this is how we create the table.

```sql
CREATE TABLE dogs (
    name VARCHAR(50) NOT NULL,
    age INT NOT NULL
);
```

```
DESC dogs;

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(50) | NO   |     | NULL    |       |
| age   | int         | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
```

<br>

### Adding DEFAULT Values


In previous table, there is **no default value**.

Define a table with a `DEFAULT` name specified:

```sql
CREATE TABLE birds (
    -> name VARCHAR(50) DEFAULT 'unknown',
    -> age INT DEFAULT 0
    -> );
```

Notice the change when you describe the table:

```
DESC birds;

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(50) | YES  |     | unknown |       |
| age   | int         | YES  |     | 0       |       |
+-------+-------------+------+-----+---------+-------+
```

Insert a bird without a name:

```
INSERT INTO birds(age) VALUES(13);

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(50) | YES  |     | unknown |       |
| age   | int         | YES  |     | 0       |       |
+-------+-------------+------+-----+---------+-------+
```

Or a nameless, ageless cat:

    INSERT INTO birds() VALUES();

<br>

#### Combine `NOT NULL` and `DEFAULT`

They are separate.
If only `default` is set, and there is no `not null`, the `null` can be set manually.


    INSERT INTO birds(name, age) VALUES(NULL, NULL);

```
SELECT * FROM birds;

+---------+------+
| name    | age  |
+---------+------+
| unknown |    3 |
| unknown |    0 |
| NULL    | NULL |
+---------+------+
```

```sql
CREATE TABLE fishes  (    
    name VARCHAR(20) NOT NULL DEFAULT 'unnamed',    
    age INT NOT NULL DEFAULT 99 
);
```

```
SELECT * FROM fishes;

Empty set (0.00 sec)
```

    INSERT INTO fishes() VALUES();

```
SELECT * FROM fishes;

+---------+-----+
| name    | age |
+---------+-----+
| unnamed |  99 |
+---------+-----+
```
<br>

### Introducing Primary Keys

Unique IDs are added to rows so we can differentiate them for every made table = **primary key**.

One way of specifying a PRIMARY KEY

```sql
CREATE TABLE unique_cats (
	cat_id INT NOT NUL PRIMARY KEY, # has to be there, has to be unique
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL
);

+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| cat_id | int         | NO   | PRI | NULL    |       |
| name   | varchar(50) | NO   |     | NULL    |       |
| age    | int         | NO   |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
```

Another option:

```sql
CREATE TABLE unique_dogs (
	dog_id INT,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    PRIMARY KEY (dog_id)
);
```

<br>

### Auto increment

- use `AUTO_INCREMENT`
- starts at `1`

```sql
CREATE TABLE unique_cats3 (
    cat_id INT AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    PRIMARY KEY (cat_id)
);

+--------+-------------+------+-----+---------+----------------+
| Field  | Type        | Null | Key | Default | Extra          |
+--------+-------------+------+-----+---------+----------------+
| dog_id | int         | NO   | PRI | NULL    | auto_increment |
| name   | varchar(50) | NO   |     | NULL    |                |
| age    | int         | NO   |     | NULL    |                |
+--------+-------------+------+-----+---------+----------------+

INSERT INTO unique_dogs(name, age) VALUES('Tina', 7);
INSERT INTO unique_dogs(name, age) VALUES('Boby', 10);

SELECT * FROM unique_dogs;

+--------+------+-----+
| dog_id | name | age |
+--------+------+-----+
|      1 | Boby |  10 |
|      2 | Tina |   7 |
+--------+------+-----+
```

<br>

## SQL FORMATTING

```sql

SELECT CONCAT(SUBSTR(title, 1, 10), '...') AS short_title FROM books;

-- or

SELECT CONCAT (
        SUBSTRING(title, 1, 10),
        '...'
    ) AS 'short_title'
FROM
    books;



SELECT 
  CONCAT(
    SUBSTR(title, 1, 10), 
    '...'
  ) AS short_title 
FROM 
  books;
```

<br>

[SQL fromatter](https://codebeautify.org/sqlformatter)