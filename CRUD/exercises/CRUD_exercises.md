# CRUD rapid fire exercises

Data to work with:

```bash
-- Create the new cats table:

CREATE TABLE cats (
    cat_id INT AUTO_INCREMENT,
    name VARCHAR(100),
    breed VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
);

-- Insert cats:

INSERT INTO cats(name, breed, age) 
VALUES ('Ringo', 'Tabby', 4),
       ('Cindy', 'Maine Coon', 10),
       ('Dumbledore', 'Maine Coon', 11),
       ('Egg', 'Persian', 4),
       ('Misty', 'Tabby', 13),
       ('George Michael', 'Ragdoll', 9),
       ('Jackson', 'Sphynx', 7);
```

<br>

## 1. SELECT and WHERE

Write the query that selects:

```bash
-- cat_id for all the rows

SELECT cat_id FROM cats_new;

+--------+
| cat_id |
+--------+
|      1 |
|      2 |
|      3 |
|      4 |
|      5 |
|      6 |
|      7 |
+--------+

-- name and breed for all the rows

SELECT name, breed FROM cats_new;

+----------------+------------+
| name           | breed      |
+----------------+------------+
| Ringo          | Tabby      |
| Cindy          | Maine Coon |
| Dumbledore     | Maine Coon |
| Egg            | Persian    |
| Misty          | Tabby      |
| George Michael | Ragdoll    |
| Jackson        | Sphynx     |
+----------------+------------+

-- just tabby breed cats and only their name and age

SELECT name, age FROM cats_new WHERE breed = 'Tabby';

+-------+------+
| name  | age  |
+-------+------+
| Ringo |    4 |
| Misty |   13 |
+-------+------+

-- cats with the cat_id that is the same as their age with only cat_id and age printed out

SELECT cat_id, AGE from CATS_NEW where cat_id = age;

+--------+------+
| cat_id | AGE  |
+--------+------+
|      4 |    4 |
|      7 |    7 |
+--------+------+

```

<br>