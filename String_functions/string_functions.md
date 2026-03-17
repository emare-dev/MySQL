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

Replaces portions of a string with other (replacement) string.

**Data in database stays the same**, only the displayed data is changed.

It is **case sensitive**.

        1. string we are operating on
        2. what we want to replace
        3. what to replace with

<br>

```sql
SELECT REPLACE('Hello, world', 'world', '$#!&'); -- Hello, $#!&
 
SELECT REPLACE('cheese bread coffee milk', ' ', ' and '); -- cheese and bread and coffee and milk

SELECT REPLACE('Hello World', 'l', '7'); -- He77o Wor7d  
 
SELECT REPLACE('Hello World', 'o', '0'); -- Hell0 W0rld
 
SELECT REPLACE('HellO World', 'o', '*'); -- HellO W*rld
 
------------

SELECT REPLACE(title, 'e ', '3') FROM books;
 
SELECT REPLACE(title, ' ', '-') FROM books;
```

<br>

## REVERSE

Takes provided string and reverses it.
It is just once for that time you do it, doesn't make permanent change.

```sql
SELECT REVERSE('Hello World'); -- !dlrow ,olleH 

SELECT REVERSE(NULL); -- NULL
 
SELECT REVERSE('meow meow');
 
SELECT REVERSE(author_fname) FROM books;
 
SELECT CONCAT('woof', REVERSE('woof'));
 
SELECT CONCAT(author_fname, REVERSE(author_fname)) FROM books;
```

<br>

## CHAR_LENGTH

Tells the number of characters in a given string.

Not the same as `LENGTH()`, which returns the length of the string as well, but in bytes.

```sql
SELECT CHAR_LENGTH('Hello World');
 
SELECT CHAR_LENGTH(title) as length, title FROM books;

+--------+-----------------------------------------------------+
| length | title                                               |
+--------+-----------------------------------------------------+
|     12 | The Namesake                                        |
|     15 | Norse Mythology                                     |
|     13 | American Gods                                       |
+--------+-----------------------------------------------------+
 
SELECT author_lname, CHAR_LENGTH(author_lname) AS 'length' FROM books;
 
SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname), ' characters long') FROM books;
```

<br>

## UPPER & LOWER

Synonyms:

        UPPER() -> UCASE()

        LOWER() -> LCASE()

```sql
SELECT UPPER('Hello World');
 
SELECT LOWER('Hello World');
 
SELECT UPPER(title) FROM books;
 
SELECT CONCAT('MY FAVORITE BOOK IS ', UPPER(title)) FROM books;
 
SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;

SELECT CONCAT('I LOVE ', UPPER(title), ' !!!') FROM books;

+----------------------------------------------------------------+
| CONCAT('I LOVE ', UPPER(title), ' !!!')                        |
+----------------------------------------------------------------+
| I LOVE THE NAMESAKE !!!                                        |
| I LOVE NORSE MYTHOLOGY !!!                                     |
| I LOVE AMERICAN GODS !!!                                       |
+----------------------------------------------------------------+
```

<br>

## Other string functions

```sql
-- insert substring into a larger string
-- 6 - at which position
-- 0 - num of characters you want to replace

SELECT INSERT('Hello Bobby', 6, 0, ' there,'); -- Hello there, Bobby

SELECT INSERT('Hello Bobby', 7, 6, 'There'); --  Hello There                      
 
-- get the leftmost or rightmost character from some string
-- num - how many leftmost or rightmost characters we want to get

SELECT LEFT('omghahalol!', 3); -- omg
SELECT RIGHT('omghahalol!', 4); -- lol!
 
SELECT LEFT(author_lname, 1) FROM books;
+-----------------------+
| LEFT(author_lname, 1) |
+-----------------------+
| L                     |
| G                     |
| G                     |
| L                     |
+-----------------------+

-- repeats a provided string the number of times provided

SELECT REPEAT('ha', 4); -- hahahaha 

-- used for removing leading or trailing spaces

SELECT TRIM('  pickle  '); -- pickle
```


<br>