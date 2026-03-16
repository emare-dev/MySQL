# String functions

[DOCUMENTATION: String functions and operators](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)

Data to work with:

```sql
CREATE TABLE books 
(
  book_id INT AUTO_INCREMENT,
  title VARCHAR(100),
  author_fname VARCHAR(100),
  author_lname VARCHAR(100),
  released_year INT,
  stock_quantity INT,
  pages INT,
  PRIMARY KEY(book_id)
);
 
INSERT INTO books (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES
  ('The Namesake', 'Jhumpa', 'Lahiri', 2003, 32, 291),
  ('Norse Mythology', 'Neil', 'Gaiman',2016, 43, 304),
  ('American Gods', 'Neil', 'Gaiman', 2001, 12, 465),
  ('Interpreter of Maladies', 'Jhumpa', 'Lahiri', 1996, 97, 198),
  ('A Hologram for the King: A Novel', 'Dave', 'Eggers', 2012, 154, 352),
  ('The Circle', 'Dave', 'Eggers', 2013, 26, 504),
  ('The Amazing Adventures of Kavalier & Clay', 'Michael', 'Chabon', 2000, 68, 634),
  ('Just Kids', 'Patti', 'Smith', 2010, 55, 304),
  ('A Heartbreaking Work of Staggering Genius', 'Dave', 'Eggers', 2001, 104, 437),
  ('Coraline', 'Neil', 'Gaiman', 2003, 100, 208),
  ('What We Talk About When We Talk About Love: Stories', 'Raymond', 'Carver', 1981, 23, 176),
  ("Where I'm Calling From: Selected Stories", 'Raymond', 'Carver', 1989, 12, 526),
  ('White Noise', 'Don', 'DeLillo', 1985, 49, 320),
  ('Cannery Row', 'John', 'Steinbeck', 1945, 95, 181),
  ('Oblivion: Stories', 'David', 'Foster Wallace', 2004, 172, 329),
  ('Consider the Lobster', 'David', 'Foster Wallace', 2005, 92, 343);
```

<br>

Alternative to copy-paste the code above:

1. You need to be in the MySQL shell, inside a database.

2. Execute all SQL statements contained in the file:

    source book_data.sql

<br>

## CONCAT

Return concatenated string.

### concat()

Example: combining author first and last name to get a full name:

    SELECT CONCAT(author_fname, ' ', author_lname) FROM books;

    +-----------------------------------------+
    | CONCAT(author_fname, ' ', author_lname) |
    +-----------------------------------------+
    | Jhumpa Lahiri                           |
    | Neil Gaiman                             |                    |
    +-----------------------------------------+

Rename the column that we get: `CONCAT(author_fname, ' ', author_lname)`

    SELECT CONCAT(author_fname, ' ', author_lname) AS author_fullname FROM books;

    +----------------------+
    | author_fullname      |
    +----------------------+
    | Jhumpa Lahiri        |
    | Neil Gaiman          |
    +----------------------+

<br>

### concat_ws()

"Concat with separator"

First argument (here: `-`) will be put between all other arguments.

```sql
SELECT
  CONCAT_WS('-',title, author_fname, author_lname)
FROM books;
```

<br>

## SUBSTRING

Takes single larger string and returns a portion of it.

Space counts!

`SUBSTR()` is a synonim

<br>


```sql
-- 'Hello World' - string we are taking from
-- 1 - starting position
-- 4 - length of the substring

SELECT SUBSTRING('Hello World', 1, 4);

+--------------------------------+
| SUBSTRING('Hello World', 1, 4) |
+--------------------------------+
| Hell                           |
+--------------------------------+
``` 

<br>

```sql 
-- if there is no 2nd number, it goes untill the end

SELECT SUBSTRING('Hello World', 7);

+------------------------------+
| SUBSTRING('Hello, world', 7) |
+------------------------------+
|  world                       |
+------------------------------+
```

```sql 
-- negative num counts backwards from the end of the string

SELECT SUBSTRING('Hello World', -3);

+-------------------------------+
| SUBSTRING('Hello, world', -3) |
+-------------------------------+
| rld                           |
+-------------------------------+
```

If you need the last character of the string, without knowing its length:

    SELECT SUBSTRING('Hello World', -1);

<br>

```sql
SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;

+-------------+
| short title |
+-------------+
| The Namesa  |
| Norse Myth  |
| American G  |
+-------------+
 
-- get first character from author's last name

SELECT SUBSTR(author_lname, 1, 1) AS initial, author_lname FROM books;

+---------+----------------+
| initial | author_lname   |
+---------+----------------+
| L       | Lahiri         |
| G       | Gaiman         |
| G       | Gaiman         |
+---------+----------------+
```

<br>

## Combining string functions

Combining `CONCAT()` and `SUBSTRING()`


```sql
SELECT CONCAT(SUBSTR(title, 1, 10), '...') AS short_title FROM books;

+---------------+
| short_title   |
+---------------+
| The Namesa... |
| Norse Myth... |
| American G... |
+---------------+
```

<br>

Combine authors' name and surname initials.

```sql
SELECT CONCAT(
    SUBSTR(author_fname, 1, 1),
    '.',
    SUBSTR(author_lname, 1, 1),
    '.'
) AS author_initials
FROM
    books;

+-----------------+
| author_initials |
+-----------------+
| J.L.            |
| N.G.            |
| N.G.            |
+-----------------+
```

<br>

## REPLACE

## REVERSE

## CHAR_LENGTH

## UPPER & LOWER

## Other string functions