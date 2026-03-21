# Agregate functions exercise

1. Print the number of books in the database.

```sql
SELECT COUNT(*) AS number_of_books FROM books;

+-----------------+
| number_of_books |
+-----------------+
|              20 |
+-----------------+
```

<br>

2. Print out how many books were released in each year. 
  Use `GROUP BY`.
  Print out on the left the year, on the right how many books were released that year.

```sql
SELECT released_year, COUNT(*) AS how_many
    -> FROM books
    -> GROUP BY released_year;

    +---------------+----------+
    | released_year | how_many |
    +---------------+----------+
    |          2003 |        2 |
    |          2016 |        1 |
    |          2001 |        3 |
    |          1996 |        1 |
    |          2012 |        1 |
    +---------------+----------+
```

<br>

3. Print out the total number of books in stock.

```sql
SELECT SUM(stock_quantity) FROM books;

    +---------------------+
    | SUM(stock_quantity) |
    +---------------------+
    |                2450 |
    +---------------------+
```

<br>

4. Find the average `released_year` for each author.
  Take into account first and last name because of duplicates.

```sql
SELECT AVG(released_year)
FROM books
GROUP BY author_lname, author_fname;

    +--------------------+
    | AVG(released_year) |
    +--------------------+
    |          1999.5000 |
    |          2006.6667 |
    |          2008.6667 |
    |          2000.0000 |
    |          2010.0000 |
    +--------------------+
```

<br>

5. Find the full name of the author who wrote the longest book.
  First name + space + last name.

```sql
SELECT CONCAT(author_fname, ' ', author_lname) AS author, pages
FROM books
WHERE pages = (SELECT MAX(pages) FROM books);

+----------------+-------+
| author         | pages |
+----------------+-------+
| Michael Chabon |   634 |
+----------------+-------+
```

<br>

6. Make this happen.

```sql
SELECT
    released_year AS year,
    COUNT(*) AS '# books',
    AVG(pages) AS 'avg pages'
FROM books
GROUP BY released_year
ORDER BY released_year;


    +------+---------+-----------+
    | year | # books | avg pages |
    +------+---------+-----------+
    | 1945 |       1 |  181.0000 |
    | 1981 |       1 |  176.0000 |
    | 1985 |       1 |  320.0000 |
    | 1989 |       1 |  526.0000 |
    | 1996 |       1 |  198.0000 |
    | 2000 |       1 |  634.0000 |
    | 2001 |       3 |  443.3333 |
    | 2003 |       2 |  249.5000 |
    | 2004 |       1 |  329.0000 |
    | 2005 |       1 |  343.0000 |
    | 2010 |       1 |  304.0000 |
    | 2012 |       1 |  352.0000 |
    | 2013 |       1 |  504.0000 |
    | 2014 |       1 |  256.0000 |
    | 2016 |       1 |  304.0000 |
    | 2017 |       1 |  367.0000 |
    +------+---------+-----------+
```

<br>