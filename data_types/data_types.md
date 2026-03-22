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

<br>

## CURDATE, CURTIME, NOW

<br>

## DATE FUNCTIONS

<br>

## TIME FUNCTIONS

<br>

## FORMATTING DATES

<br>

## DATE MATH

<br>

## TIMESTAMPS

<br>

## DEFAULT AND ON UPDATE TIMESTAMPS

<br>