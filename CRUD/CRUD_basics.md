# CRUD basics

C - create

R - read

U - update

D - delete

4 basic actions done with data.

## R - READING 

How to retrieve, search and read data that is already in the table?

<br>

### SELECT

One can select **every column** or just a **specific column**.
Each time, **all the rows** are shown. 

```bash
SELECT * FROM cats; -- Get all columns

SELECT age FROM cats; -- Only get the age column

SELECT name, breed FROM cats; -- Select multiple specific columns
```

<br>

### WHERE

Used in SQL to narrow down **rows** you are working with.

Specifies a **condition**.

Can be used for selecting, updating and deleting rows.

```bash

SELECT * FROM cats WHERE age = 4;
    
+--------+-------+---------+------+
| cat_id | name  | breed   | age  |
+--------+-------+---------+------+
|      1 | Ringo | Tabby   |    4 |
|      4 | Egg   | Persian |    4 |
+--------+-------+---------+------+

SELECT name, age FROM cats WHERE age = 4;

+-------+------+
| name  | age  |
+-------+------+
| Ringo |    4 |
| Egg   |    4 |
+-------+------+


SELECT name FROM cats WHERE age = 4;

+-------+
| name  |
+-------+
| Ringo |
| Egg   |
+-------+


SELECT * FROM cats WHERE name ='Egg'; -- here it is case insensitive

+--------+------+---------+------+
| cat_id | name | breed   | age  |
+--------+------+---------+------+
|      4 | Egg  | Persian |    4 |
+--------+------+---------+------+
```

<br>

### Aliases

When selecting data, rename a column in the output result to make it shorter/easier to understand.

**It is temporary.**

Used also for results that don't have a name.

Use 'AS' to alias a column in your results (it doesn't actually change the name of the column in the table)

```bash
-- instead of:

SELECT cat_id, name FROM cats_new;
+--------+----------------+
| cat_id | name           |
+--------+----------------+
|      1 | Ringo          |
|      2 | Cindy          |
|      3 | Dumbledore     |
|      4 | Egg            |
|      5 | Misty          |
|      6 | George Michael |
|      7 | Jackson        |
+--------+----------------+

-- use this only for this output, this time only:

SELECT cat_id AS id, name FROM cats;

+----+
| id |
+----+
|  1 |
|  2 |
|  3 |
|  4 |
|  5 |
|  6 |
|  7 |
+----+
```

<br><br>

## U - UPDATE

Pair: `UPDATE` ... `SET`

- **what** are we updating
- **on which rows**

**Rule of thumb**

  ⚠️ SELECT BEFORE UPDATE

<br>

Change tabby cats to shorthair:

    UPDATE cats SET breed='Shorthair' WHERE breed='Tabby';

Another update:

    UPDATE cats SET age=14 WHERE name='Misty';

Update multiple fields at once:

    UPDATE employees SET current_status = 'fired', last_name = 'Doe';

<br>

## D - DELETE

    DELETE FROM <table> WHERE <condition>;

```bash
DELETE FROM cats; -- Clears the whole table (deletes all rows in the cats table)

DELETE FROM cats WHERE name='Egg'; -- Delete all cats with name of 'Egg'
```

<br>