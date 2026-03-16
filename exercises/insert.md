# Insert exercise

Create a table called `owners`.

- first_name - 20 char limit
- last_name - 20 char limit
- age

Insert 2 people separatelly:

    Tina Belcher, 13
    Bob Belcher, 25

Insert 3 people in one go:

    Linda Belcher, 45
    Phillip Frond, 38
    Calvin Fishoeder, 70

<br>

```sql
# create table OWNERS
CREATE TABLE owners (
    -> first_name VARCHAR(20),
    -> last_name VARCHAR(20),
    -> age INT
    -> );

# see the created table
DESC owners;

# add 2 people separatelly
INSERT INTO owners (first_name, last_name, age) VALUES ('Tina', 'Belcher', 13);

INSERT INTO owners (first_name, last_name, age) VALUES ('Bob', 'Belcher', 25);

# add multiple people in one go
INSERT INTO owners (first_name, last_name, age)
    -> VALUES 
    -> ('Linda', 'Belcher', 45),
    -> ('Phillip', 'Frond',38),
    -> ('Calvin', 'Fishoeder',70);

# see the table

SELECT * FROM owners;
# +------------+-----------+------+
# | first_name | last_name | age  |
# +------------+-----------+------+
# | Tina       | Belcher   |   13 |
# | Bob        | Belcher   |   25 |
# | Bob        | Belcher   |   25 |
# | Linda      | Belcher   |   45 |
# | Phillip    | Frond     |   38 |
# | Calvin     | Fishoeder |   70 |
# +------------+-----------+------+
# 6 rows in set (0.00 sec)
```