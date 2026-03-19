# Advanced selections

Narrowing, refining, manipulationg selections.

See [SELECT](https://dev.mysql.com/doc/refman/9.6/en/select.html) documentation.

## DISTINCT

Goes after `SELECT`, before a column name.

```sql
SELECT author_lname FROM books; -- shows ALL (with duplicates)
SELECT DISTINCT author_lname FROM books; -- removes duplicates
 
SELECT author_fname, author_lname FROM books; -- shows ALL first and last names, with duplicates
 
-- solutions to get rid of duplicates
SELECT DISTINCT CONCAT(author_fname,' ', author_lname) AS 'full name' FROM books;

+----------------------+
| full name            |
+----------------------+
| Jhumpa Lahiri        |
| Neil Gaiman          |
| Dave Eggers          |
| Michael Chabon       |
| Patti Smith          |
| Raymond Carver       |
| Don DeLillo          |
| John Steinbeck       |
| David Foster Wallace |
| Dan Harris           |
| Freida Harris        |
| George Saunders      |
+----------------------+
 
SELECT DISTINCT author_fname, author_lname FROM books;

+--------------+----------------+
| author_fname | author_lname   |
+--------------+----------------+
| Jhumpa       | Lahiri         |
| Neil         | Gaiman         |
| Dave         | Eggers         |
| Michael      | Chabon         |
| Patti        | Smith          |
| Raymond      | Carver         |
| Don          | DeLillo        |
| John         | Steinbeck      |
| David        | Foster Wallace |
| Dan          | Harris         |
| Freida       | Harris         |
| George       | Saunders       |
+--------------+----------------+
```

If we print 3 different columns with DISTINCT, to get rid of duplicates, all 3 columns would have to be the same to be considered duplicates, otherwise they will be printed.

<br>

## ORDER BY

Sorting results.
Comes **after** the select.

By default: A -> Z
`DESC`: Z -> A

```sql
SELECT * FROM books
ORDER BY author_lname;
 
SELECT * FROM books
ORDER BY author_lname DESC;
 
-- this still works, although we won't see the released year
SELECT * FROM books
ORDER BY released_year;

SELECT title, pages FROM books
ORDER BY pages;

-- order by the 2nd column: goed through 2nd column from A-Z
SELECT book_id, author_fname, author_lname, pages
FROM books ORDER BY 2;

SELECT book_id, author_fname, author_lname, pages
FROM books ORDER BY 2 DESC;
 
-- order by multiple columns: it sorts by the first ennumerated, then goes to the next
-- makes sense if you have the same author with multiple works
SELECT book_id, author_fname, author_lname, pages
FROM books ORDER BY author_lname, author_fname;
```

<br>

## LIMIT

<br>

## LIKE

<br>

## 

<br>

## 

<br>