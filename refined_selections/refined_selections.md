# Refined selections

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

-- order by columns that aren't part of the table, but are results we asked SQL for
SELECT CONCAT(author_lname, ', ', author_fname) AS 'author' FROM books ORDER BY author;

+-----------------------+
| author                |
+-----------------------+
| Carver, Raymond       |
| Carver, Raymond       |
| Chabon, Michael       |
| DeLillo, Don          |
| Eggers, Dave          |
| Eggers, Dave          |
| Eggers, Dave          |
| Foster Wallace, David |
| Foster Wallace, David |
| Gaiman, Neil          |
| Gaiman, Neil          |
| Gaiman, Neil          |
| Harris, Dan           |
| Harris, Freida        |
| Lahiri, Jhumpa        |
| Lahiri, Jhumpa        |
| Saunders, George      |
| Smith, Patti          |
| Steinbeck, John       |
+-----------------------+
```

<br>

## LIMIT

Controls the number of results we get back.

`LIMIT` + `num` limits the results we get back.

Often used with `ORDER`

```sql
SELECT title FROM books LIMIT 3;
 
SELECT title FROM books LIMIT 1;
 
SELECT title FROM books LIMIT 10;
 
SELECT * FROM books LIMIT 1;
 
-- first books sorted by the released year
SELECT title, released_year FROM books 
ORDER BY released_year LIMIT 5;
 
SELECT title, released_year FROM books 
ORDER BY released_year DESC LIMIT 1;
 
-- TELL IT AT WHICH POINT TO START

-- goes from 0 to 5
SELECT title, released_year FROM books 
ORDER BY released_year DESC LIMIT 0,5;
 
-- start at 1, go to 5
SELECT title, released_year FROM books 
ORDER BY released_year DESC LIMIT 1,3;
 
SELECT title, released_year FROM books 
ORDER BY released_year DESC LIMIT 10,1;
 
SELECT * FROM books LIMIT 95,18446744073709551615; -- Empty set (0.00 sec)

-- gives as much as it can
SELECT * FROM books LIMIT 40;
 
SELECT title FROM books LIMIT 5;
 
SELECT title FROM books LIMIT 5, 123219476457;
 
SELECT title FROM books LIMIT 5, 50;
```

<br>

## LIKE

Operator for basic sarching.

wild cards:

```sql
-- ANY
-- zero / more characters + some word + zero / more characters
% %

-- VERY SPECIFIC
-- exactly that much character as the number of underscores
_ 
```


```sql
-- exact match
SELECT title, author_fname, author_lname
FROM books
WHERE author_fname='David';

+----------------------+--------------+----------------+
| title                | author_fname | author_lname   |
+----------------------+--------------+----------------+
| Oblivion: Stories    | David        | Foster Wallace |
| Consider the Lobster | David        | Foster Wallace |
+----------------------+--------------+----------------+

-- not exact match
SELECT title, author_fname, author_lname, pages 
FROM books
WHERE author_fname LIKE '%da%';

+-------------------------------------------+--------------+----------------+
| title                                     | author_fname | author_lname   |
+-------------------------------------------+--------------+----------------+
| A Hologram for the King: A Novel          | Dave         | Eggers         |
| The Circle                                | Dave         | Eggers         |
| A Heartbreaking Work of Staggering Genius | Dave         | Eggers         |
| Oblivion: Stories                         | David        | Foster Wallace |
| Consider the Lobster                      | David        | Foster Wallace |
| 10% Happier                               | Dan          | Harris         |
| fake_book                                 | Freida       | Harris         |
+-------------------------------------------+--------------+----------------+
 

 
SELECT * FROM books
WHERE author_fname LIKE '____'; -- author first name is exactly 4 characters

+---------+-------------+--------------+--------------+---------------+----------------+-------+
| book_id | title       | author_fname | author_lname | released_year | stock_quantity | pages |
+---------+-------------+--------------+--------------+---------------+----------------+-------+
|      13 | White Noise | Don          | DeLillo      |          1985 |             49 |   320 |
|      17 | 10% Happier | Dan          | Harris       |          2014 |             29 |   256 |
+---------+-------------+--------------+--------------+---------------+----------------+-------+

-- exactly 3 characters total, the second character must be "a"
SELECT * FROM books
WHERE author_fname LIKE '_a_';
```
<br>

### Escaping wildcards

When you want to match a string with '%' sign, use `\`: LIKE '%\%%'`

```sql
-- To select books with '%' in their title:
SELECT * FROM books
WHERE title LIKE '%\%%';
 
-- To select books with an underscore '_' in title:
SELECT * FROM books
WHERE title LIKE '%\_%';
```

<br>