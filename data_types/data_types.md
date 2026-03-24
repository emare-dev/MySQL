# Revisiting data types

The most important ones:

- [CHAR vs VARCHAR](#char-vs-varchar)
- [INT, TINYINT, BIGINT](#int-tinyint-bigint)
- [DECIMAL](#decimal)
- [FLOAT and DOUBLE](#float-and-double)
- [DATE and TIME](#date-and-time)
- [CURDATE, CURTIME, NOW](#curdate-curtime-now)
- [DATE FUNCTIONS](#date-functions)
- [TIME FUNCTIONS](#time-functions)
- [FORMATTING DATES](#formatting-dates)
- [DATE MATH](#date-math)
- [TIMESTAMPS](#timestamps)
- [DEFAULT AND ON UPDATE TIMESTAMPS](#default-and-on-update-timestamps)

<br>

[Data types documentation](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)

<br>

## CHAR vs VARCHAR

String data types.
Differ in max length, the way they are stored and retrieved and when they are used.

### CHAR

Have a fixed length: if it is 2, every stored string will be the size of 2 characters, no matter if it is longer.

Use it when your data is similar in size.

- state abbreviations
- post/zip codes
- yes/no flags

### VARCHAR

Has more flexibility if data varies in size.

<br>

## INT, TINYINT, BIGINT ...

<br>

## DECIMAL

`DECIMAL(5, 2)` 

5 - up to this total number of digits
2 - how many come after a decimal

`999,99` or `1,1` would both be valid

```sql
CREATE TABLE producs (price DECIMAL(5,2));

INSERT INTO products (price) VALUES (4.50);
```

<br>

## FLOAT and DOUBLE

Decimal can be more exact, is very precise, but takes up more space.

Float/double can store larger nubers using less space, but not as precise.

Double takes 2x more space than float.

<br>

## DATE and TIME

`DATE`: YYYY-MM-DD

`TIME`: HH:MM:SS

`DATETIME`: YYYY-MM-DD HH:MM:SS

<br>

## WORKING WITH DATES

```sql
CREATE TABLE people (
	name VARCHAR(100),
    birthdate DATE,
    birthtime TIME,
    birthdt DATETIME
);
 
INSERT INTO people (name, birthdate, birthtime, birthdatetime)
VALUES ('Elton', '2000-12-25', '11:00:00', '2000-12-25 11:00:00');
 
INSERT INTO people (name, birthdate, birthtime, birthdatetime)
VALUES ('Lulu', '1985-04-11', '9:45:10', '1985-04-11 9:45:10');
 
INSERT INTO people (name, birthdate, birthtime, birthdatetime)
VALUES ('Juan', '2020-08-15', '23:59:00', '2020-08-15 23:59:00');
```

<br>

## CURDATE, CURTIME, NOW

Get actual curent date/time dynamically.

```sql
SELECT CURTIME();
 
SELECT CURDATE();
 
-- short for CURRENT_TIMESTAMPE()
SELECT NOW(); -- 2026-03-22 21:04:29
 
INSERT INTO people (name, birthdate, birthtime, birthdatetime)
VALUES ('Hazel', CURDATE(), CURTIME(), NOW());
```

<br>

## DATE FUNCTIONS

Formatting dates or extracting date into a different format.

`DAY()` synonsm for `DAYOFMONTH()` 

```sql
SELECT birthdate, DAY(birthdate) FROM people;

+------------+----------------+
| birthdate  | DAY(birthdate) |
+------------+----------------+
| 2000-12-25 |             25 |
| 1985-04-11 |             11 |
| 2020-08-15 |             15 |
| 2026-03-22 |             22 |
+------------+----------------+


SELECT birthdate, DAY(birthdate), DAYOFWEEK(birthdate) FROM people;

+------------+----------------+----------------------+
| birthdate  | DAY(birthdate) | DAYOFWEEK(birthdate) |
+------------+----------------+----------------------+
| 2000-12-25 |             25 |                    2 |
| 1985-04-11 |             11 |                    5 |
| 2020-08-15 |             15 |                    7 |
| 2026-03-22 |             22 |                    1 |
+------------+----------------+----------------------+



SELECT 
    birthdate,
    DAY(birthdate),
    DAYOFWEEK(birthdate),
    DAYOFYEAR(birthdate)
FROM people;

+------------+----------------+----------------------+----------------------+
| birthdate  | DAY(birthdate) | DAYOFWEEK(birthdate) | DAYOFYEAR(birthdate) |
+------------+----------------+----------------------+----------------------+
| 2000-12-25 |             25 |                    2 |                  360 |
| 1985-04-11 |             11 |                    5 |                  101 |
| 2020-08-15 |             15 |                    7 |                  228 |
| 2026-03-22 |             22 |                    1 |                   81 |
+------------+----------------+----------------------+----------------------+

 
SELECT 
    birthdate,
    MONTHNAME(birthdate),
    YEAR(birthdate)
FROM people;

+------------+----------------------+-----------------+
| birthdate  | MONTHNAME(birthdate) | YEAR(birthdate) |
+------------+----------------------+-----------------+
| 2000-12-25 | December             |            2000 |
| 1985-04-11 | April                |            1985 |
| 2020-08-15 | August               |            2020 |
| 2026-03-22 | March                |            2026 |
+------------+----------------------+-----------------+
```

<br>

## TIME FUNCTIONS

Getting the minute or hour from a time.
It is SINGULAR.

```sql
SELECT 
    birthtime,
    HOUR(birthtime),
    MINUTE(birthtime)
FROM people;

+-----------+-----------------+-------------------+
| birthtime | HOUR(birthtime) | MINUTE(birthtime) |
+-----------+-----------------+-------------------+
| 11:00:00  |              11 |                 0 |
| 09:45:10  |               9 |                45 |
| 23:59:00  |              23 |                59 |
| 21:05:00  |              21 |                 5 |
+-----------+-----------------+-------------------+
 

SELECT 
    birthdatetime,
    MONTH(birthdatetime),
    DAY(birthdatetime),
    HOUR(birthdatetime),
    MINUTE(birthdatetime)
FROM people;

+---------------------+----------------------+--------------------+---------------------+-----------------------+
| birthdatetime       | MONTH(birthdatetime) | DAY(birthdatetime) | HOUR(birthdatetime) | MINUTE(birthdatetime) |
+---------------------+----------------------+--------------------+---------------------+-----------------------+
| 2000-12-25 11:00:00 |                   12 |                 25 |                  11 |                     0 |
| 1985-04-11 09:45:10 |                    4 |                 11 |                   9 |                    45 |
| 2020-08-15 23:59:00 |                    8 |                 15 |                  23 |                    59 |
| 2026-03-22 21:05:00 |                    3 |                 22 |                  21 |                     5 |
+---------------------+----------------------+--------------------+---------------------+-----------------------+
```

<br>

## FORMATTING DATES

How to get this format: `April 11, 1989`

```sql
SELECT MONTHNAME(birthdate), DAY(birthdate), YEAR(birthdate) FROM people;

+----------------------+----------------+-----------------+
| MONTHNAME(birthdate) | DAY(birthdate) | YEAR(birthdate) |
+----------------------+----------------+-----------------+
| December             |             25 |            2000 |
| April                |             11 |            1985 |
| August               |             15 |            2020 |
| March                |             22 |            2026 |
+----------------------+----------------+-----------------+
```

Better way: `DATE_FORMAT(birthdate, format string)`

We are passing [specifier characters/sequences](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format) as arguments.

<br>

```sql
SELECT DATE_FORMAT(birthdate, '%b') FROM people;

+------------------------------+
| DATE_FORMAT(birthdate, '%b') |
+------------------------------+
| Dec                          |
| Apr                          |
| Aug                          |
| Mar                          |
+------------------------------+


SELECT birthdate, DATE_FORMAT(birthdate, '%a %b %D') FROM people;

+------------+------------------------------------+
| birthdate  | DATE_FORMAT(birthdate, '%a %b %D') |
+------------+------------------------------------+
| 2000-12-25 | Mon Dec 25th                       |
| 1985-04-11 | Thu Apr 11th                       |
| 2020-08-15 | Sat Aug 15th                       |
| 2026-03-22 | Sun Mar 22nd                       |
+------------+------------------------------------+
 

SELECT birthdatetime, DATE_FORMAT(birthdatetime, '%H:%i') FROM people;

+---------------------+-------------------------------------+
| birthdatetime       | DATE_FORMAT(birthdatetime, '%H:%i') |
+---------------------+-------------------------------------+
| 2000-12-25 11:00:00 | 11:00                               |
| 1985-04-11 09:45:10 | 09:45                               |
| 2020-08-15 23:59:00 | 23:59                               |
| 2026-03-22 21:05:00 | 21:05                               |
+---------------------+-------------------------------------+
 

SELECT birthdatetime, DATE_FORMAT(birthdatetime, 'BORN ON: %r') FROM people;

+---------------------+-------------------------------------------+
| birthdatetime       | DATE_FORMAT(birthdatetime, 'BORN ON: %r') |
+---------------------+-------------------------------------------+
| 2000-12-25 11:00:00 | BORN ON: 11:00:00 AM                      |
| 1985-04-11 09:45:10 | BORN ON: 09:45:10 AM                      |
| 2020-08-15 23:59:00 | BORN ON: 11:59:00 PM                      |
| 2026-03-22 21:05:00 | BORN ON: 09:05:00 PM                      |
+---------------------+-------------------------------------------+
```

<br>

## DATE MATH

<br>

## TIMESTAMPS

<br>

## DEFAULT AND ON UPDATE TIMESTAMPS

<br>