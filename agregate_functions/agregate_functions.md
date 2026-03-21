# Agregate functions
 
Different ways of performing analysis on data.

Can operate on multiple rows and pieces of data at once

[Agregate functions docs](https://dev.mysql.com/doc/refman/8.4/en/aggregate-functions.html)

<br>

## Count basics

Built in MySQL.

Shows **how many values are in a column**

`DISTINCT` used for counting unique values (the ones that show multiple times only counted once).

```sql
SELECT COUNT(*) FROM books; -- select number of rows from books

+----------+
| COUNT(*) |
+----------+
|       19 |
+----------+
 
-- count number of author first names
-- counts every time a value is present in that coulmn
SELECT COUNT(author_lname) FROM books;
 
-- 
SELECT COUNT(DISTINCT author_lname) FROM books;
 
+------------------------------+
| COUNT(DISTINCT author_lname) |
+------------------------------+
|                           11 |
+------------------------------+

-- how many titles CONTAIN the word "the"
SELECT title FROM books WHERE title LIKE '%the%';

+-------------------------------------------+
| title                                     |
+-------------------------------------------+
| The Namesake                              |
| A Hologram for the King: A Novel          |
| The Circle                                |
| The Amazing Adventures of Kavalier & Clay |
| Consider the Lobster                      |
| Lincoln In The Bardo                      |
+-------------------------------------------+


-- count how many rows we got back
SELECT COUNT(*) FROM books WHERE title LIKE '%the%';
+----------+
| COUNT(*) |
+----------+
|        6 |
+----------+
```

<br>

## GROUP BY

One of the most important and most useful functions.

It summarizes/agregates identical data into single rows and keeps it in memory.

```sql
-- groups internally based upon autor last name
SELECT title, author_lname FROM books GROUP BY author_lname;


-- count how many books each author has written
-- groupo all of the rows together by the author's last name, select author's last name from each of those groups and then count the rows of each group
SELECT author_lname, COUNT(*) 
FROM books
GROUP BY author_lname;

    +----------------+----------+
    | author_lname   | COUNT(*) |
    +----------------+----------+
    | Lahiri         |        2 |
    | Gaiman         |        3 |
    | Eggers         |        3 |
    | Chabon         |        1 |
    | Smith          |        1 |
    | Carver         |        2 |
    | DeLillo        |        1 |
    | Steinbeck      |        1 |
    | Foster Wallace |        2 |
    | Harris         |        2 |
    | Saunders       |        1 |
    +----------------+----------+


SELECT 
    author_lname, COUNT(*) AS books_written
FROM
    books
GROUP BY author_lname
ORDER BY books_written DESC;

    +----------------+---------------+
    | author_lname   | books_written |
    +----------------+---------------+
    | Gaiman         |             3 |
    | Eggers         |             3 |
    | Lahiri         |             2 |
    | Carver         |             2 |
    | Foster Wallace |             2 |
    | Harris         |             2 |
    | Chabon         |             1 |
    | Smith          |             1 |
    | DeLillo        |             1 |
    | Steinbeck      |             1 |
    | Saunders       |             1 |
    +----------------+---------------+


-- group by released year (there are 16)
-- counts the number of yrows in each year
SELECT released_year, COUNT(*) FROM books GROUP BY released_year;

    +---------------+----------+
    | released_year | COUNT(*) |
    +---------------+----------+
    |          2003 |        2 |
    |          2016 |        1 |
    |          2001 |        3 |
    |          1996 |        1 |
    |          2012 |        1 |
    |          2013 |        1 |
    |          2000 |        1 |
    |          2010 |        1 |
    |          1981 |        1 |
    |          1989 |        1 |
    |          1985 |        1 |
    |          1945 |        1 |
    |          2004 |        1 |
    |          2005 |        1 |
    |          2014 |        1 |
    |          2017 |        1 |
    +---------------+----------+


SELECT * FROM books GROUP BY author_lname; -- gives an error; option to change SQL mode
```

<br>

## MIN and MAX basics

- `MIN()` find a minimum value in a column or group

- `MAX()` find a maximum value in a column or group

Usually used for numerical values.

<br>

```sql
-- find minimum released year
SELECT MIN(released_year) FROM books;

-- find the most number of pages
SELECT MAX(pages) FROM books;
 
-- MIN and MAX combined
SELECT MIN(author_lname), MAX(author_lname) FROM books;
+-------------------+-------------------+
| MIN(author_lname) | MAX(author_lname) |
+-------------------+-------------------+
| Carver            | Steinbeck         |
+-------------------+-------------------+

```

<br>

## Subqueries

They evaluate first, then the rest of the expression.

```sql
-- get the title of the longest book if I don't know the exact number of pages
SELECT title, pages FROM books
ORDER BY pages DESC LIMIT 1;

-- option with SUBQUERY
-- if there is a duplicate of same num of pages, it will print it, too
SELECT title, pages FROM books
WHERE pages = (SELECT MAX(pages) FROM books);

        +-------------------------------------------+-------+
        | title                                     | pages |
        +-------------------------------------------+-------+
        | The Amazing Adventures of Kavalier & Clay |   634 |
        +-------------------------------------------+-------+


-- find the title of the book that was released earliest
SELECT MIN(released_year) FROM books;
 
SELECT title, released_year FROM books 
WHERE released_year = (SELECT MIN(released_year) FROM books);

        +-------------+---------------+
        | title       | released_year |
        +-------------+---------------+
        | Cannery Row |          1945 |
        +-------------+---------------+
```

<br>

## Grouping by multiple columns 

<br>

## MIN and MAX with GROUP BY

<br>

## SUM

<br>

## AVG

<br>
