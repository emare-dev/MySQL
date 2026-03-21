# Agregate functions
 
Different ways of performing analysis on data.

Can operate on multiple rows and pieces of data at once

[Agregate functions docs](https://dev.mysql.com/doc/refman/8.4/en/aggregate-functions.html)

<br>

## Count basics

Built in MySQL.

Shows **how many values are in a column**.

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

```sql
-- group books by author, show how many books each author has
SELECT author_fname, author_lname, COUNT(*) 
FROM books 
GROUP BY author_lname, author_fname;

    +--------------+----------------+----------+
    | author_fname | author_lname   | COUNT(*) |
    +--------------+----------------+----------+
    | Jhumpa       | Lahiri         |        2 |
    | Neil         | Gaiman         |        3 |
    | Dave         | Eggers         |        3 |
    | Michael      | Chabon         |        1 |
    | Patti        | Smith          |        1 |
    | Raymond      | Carver         |        2 |
    | Don          | DeLillo        |        1 |
    | John         | Steinbeck      |        1 |
    | David        | Foster Wallace |        2 |
    | Dan          | Harris         |        1 |
    | Freida       | Harris         |        1 |
    | George       | Saunders       |        1 |
    | NULL         | NULL           |        1 |
    +--------------+----------------+----------+
 
 
SELECT CONCAT(author_fname, ' ', author_lname) AS author,  COUNT(*)
FROM books
GROUP BY author;

    +----------------------+----------+
    | author               | COUNT(*) |
    +----------------------+----------+
    | Jhumpa Lahiri        |        2 |
    | Neil Gaiman          |        3 |
    | Dave Eggers          |        3 |
    | Michael Chabon       |        1 |
    | Patti Smith          |        1 |
    | Raymond Carver       |        2 |
    | Don DeLillo          |        1 |
    | John Steinbeck       |        1 |
    | David Foster Wallace |        2 |
    | Dan Harris           |        1 |
    | Freida Harris        |        1 |
    | George Saunders      |        1 |
    | NULL                 |        1 |
    +----------------------+----------+
```

<br>

## MIN and MAX with GROUP BY

```sql
-- find the year each author publiched their first book
-- group all the books by the same author together and then find the minimum year for that author
SELECT author_lname, MIN(released_year) FROM books GROUP BY author_lname;
 
        +----------------+--------------------+
        | author_lname   | MIN(released_year) |
        +----------------+--------------------+
        | Lahiri         |               1996 |
        | Gaiman         |               2001 |
        | Eggers         |               2001 |
        | Chabon         |               2000 |
        | Smith          |               2010 |
        | Carver         |               1981 |
        | DeLillo        |               1985 |
        | Steinbeck      |               1945 |
        | Foster Wallace |               2004 |
        | Harris         |               2001 |
        | Saunders       |               2017 |
        | NULL           |               NULL |
        +----------------+--------------------+

SELECT author_lname, MAX(released_year), MIN(released_year) FROM books GROUP BY author_lname;

        +----------------+--------------------+--------------------+
        | author_lname   | MIN(released_year) | MAX(released_year) |
        +----------------+--------------------+--------------------+
        | Lahiri         |               1996 |               2003 |
        | Gaiman         |               2001 |               2016 |
        | Eggers         |               2001 |               2013 |
        | Chabon         |               2000 |               2000 |
        | Smith          |               2010 |               2010 |
        | Carver         |               1981 |               1989 |
        | DeLillo        |               1985 |               1985 |
        | Steinbeck      |               1945 |               1945 |
        | Foster Wallace |               2004 |               2005 |
        | Harris         |               2001 |               2014 |
        | Saunders       |               2017 |               2017 |
        | NULL           |               NULL |               NULL |
        +----------------+--------------------+--------------------+
 

SELECT 
	author_lname, 
	COUNT(*) as books_written, 
	MAX(released_year) AS latest_release,
	MIN(released_year)  AS earliest_release,
      MAX(pages) AS longest_page_count
FROM books GROUP BY author_lname;

        +----------------+---------------+----------------+------------------+--------------------+
        | author_lname   | books_written | latest_release | earliest_release | longest_page_count |
        +----------------+---------------+----------------+------------------+--------------------+
        | Lahiri         |             2 |           2003 |             1996 |                291 |
        | Gaiman         |             3 |           2016 |             2001 |                465 |
        | Eggers         |             3 |           2013 |             2001 |                504 |
        | Chabon         |             1 |           2000 |             2000 |                634 |
        | Smith          |             1 |           2010 |             2010 |                304 |
        | Carver         |             2 |           1989 |             1981 |                526 |
        | DeLillo        |             1 |           1985 |             1985 |                320 |
        | Steinbeck      |             1 |           1945 |             1945 |                181 |
        | Foster Wallace |             2 |           2005 |             2004 |                343 |
        | Harris         |             2 |           2014 |             2001 |                428 |
        | Saunders       |             1 |           2017 |             2017 |                367 |
        | NULL           |             1 |           NULL |             NULL |                634 |
        +----------------+---------------+----------------+------------------+--------------------+


SELECT 
	author_lname, author_fname,
	COUNT(*) as books_written, 
	MAX(released_year) AS latest_release,
	MIN(released_year)  AS earliest_release
FROM books GROUP BY author_lname, author_fname;

+----------------+--------------+---------------+----------------+------------------+
| author_lname   | author_fname | books_written | latest_release | earliest_release |
+----------------+--------------+---------------+----------------+------------------+
| Lahiri         | Jhumpa       |             2 |           2003 |             1996 |
| Gaiman         | Neil         |             3 |           2016 |             2001 |
| Eggers         | Dave         |             3 |           2013 |             2001 |
| Chabon         | Michael      |             1 |           2000 |             2000 |
| Smith          | Patti        |             1 |           2010 |             2010 |
| Carver         | Raymond      |             2 |           1989 |             1981 |
| DeLillo        | Don          |             1 |           1985 |             1985 |
| Steinbeck      | John         |             1 |           1945 |             1945 |
| Foster Wallace | David        |             2 |           2005 |             2004 |
| Harris         | Dan          |             1 |           2014 |             2014 |
| Harris         | Freida       |             1 |           2001 |             2001 |
| Saunders       | George       |             1 |           2017 |             2017 |
+----------------+--------------+---------------+----------------+------------------+
```

<br>

## SUM

```sql
-- summs all pages of the books in the entire table
SELECT SUM(pages) FROM books;
 
-- sum all pages for each author
SELECT author_lname, SUM(pages) FROM books GROUP BY author_lname;

        +----------------+------------+
        | author_lname   | SUM(pages) |
        +----------------+------------+
        | Lahiri         |        489 |
        | Gaiman         |        977 |
        | Eggers         |       1293 |
        | Chabon         |        634 |
        +----------------+------------+

-- sum pages by author, count how many books there are
SELECT author_lname, COUNT(*), SUM(pages)
FROM books
GROUP BY author_lname;

-- will sum up to 0
SELECT SUM(author_lname) FROM books;
```

<br>

## AVG

Can find average across all groups/data sets or group something and then find the average.

```sql
-- 
SELECT AVG(pages) FROM books;
 
-- finds average released year of all books
SELECT AVG(released_year) FROM books;
 
-- average stock quantity for all books released in the same year
SELECT 
    released_year, 
    AVG(stock_quantity), 
    COUNT(*) FROM books
GROUP BY released_year;

    +---------------+---------------------+----------+
    | released_year | AVG(stock_quantity) | COUNT(*) |
    +---------------+---------------------+----------+
    |          2003 |             66.0000 |        2 |
    |          2016 |             43.0000 |        1 |
    |          2001 |            134.3333 |        3 |
    |          1996 |             97.0000 |        1 |
    |          2012 |            154.0000 |        1 |
    |          2013 |             26.0000 |        1 |
    +---------------+---------------------+----------+
```
<br>
