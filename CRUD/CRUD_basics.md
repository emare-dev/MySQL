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