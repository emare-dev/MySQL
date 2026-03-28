## Data types exercise

1. What's a good use case for CHAR?

  For when data is similar in size: state abbreviations, postal/zip codes, YES/NO flags...

<br>

2. Fill in the blanks (price is always < 1,000,000).

```sql
CREATE TABLE inventory (
    item_name VARCHAR(100),
    price DECIMAL(8,2),
    quantity INT
);
```
<br>

3. What's the difference between `DATETIME` and `TIMESTAMP`?

  Both store date–time values, 
  differ in range, storage, time zone handling, and behavior.

  `DATETIME` for fixed values (no timezone shifts).
  `TIMESTAMP` for timezone-aware event tracking.

<br>

| Feature            | `DATETIME`                   | `TIMESTAMP`                            |
| ------------------ | ---------------------------- | -------------------------------------- |
| Time zone handling | Stored as-is (no conversion) | Stored in UTC, auto-converted          |
| Range              | 1000–9999                    | 1970–2038                              |
| Storage            | ~5 bytes                     | 4 bytes                                |
| Auto update        | Manual (explicit config)     | Built-in support (`CURRENT_TIMESTAMP`) |
| Use case           | Scheduled/local times        | System logs, real-time events          |


<br>

4. Print out the current time.
5. Print out the current date (without time).

```sql
SELECT NOW() -- 2026-03-28 12:37:27
-- CURRENT_TIMESTAMP() gives same result

SELECT CURTIME() -- 12:37:54 
SELECT CURDATE() -- 2026-03-28
```

<br>

6. Print out the current day of the week (the number).

```sql
-- 1–7
-- Sunday = 1, Monday = 2, … Saturday = 7
SELECT DAYOFWEEK(NOW());

+------------------+
| DAYOFWEEK(NOW()) |
+------------------+
|                7 |
+------------------+

or
-- 0–6
-- Monday = 0, … Sunday = 6
SELECT WEEKDAY(NOW());

+----------------+
| WEEKDAY(NOW()) |
+----------------+
|              5 |
+----------------+
```

<br>

7. Print out the current day of the week (the day name).

```sql
SELECT DAYNAME(NOW()); -- Saturday
```

<br>

8. Print out the current day and time using this format: `mm/dd/yyyy`.

```sql
SELECT DATE_FORMAT(NOW(), '%m/%d/%Y'); -- 03/28/2026
```

<br>

9. Print out the current day and time using this format:

    January 2nd at 3:15
    April 1st at 10:18

```sql
-- %M → Month name (January)
-- %D → Day with suffix (2nd, 1st)
-- %H:%i → Time (24-hour)
-- %l → Hour (1–12, no leading zero)
SELECT DATE_FORMAT(NOW(), '%M %D at %l:%i'); -- March 28th at 12:46
```

<br>

10. Create a tweets table that stores:

- The Tweet content
- A Username
- Time it was created

```sql
CREATE TABLE tweets (
  content VARCHAR(200),
  username VARCHAR(50),
  created_at TIMESTAMP default NOW();
);

INSERT INTO tweets(content, username)
       VALUES('This is my first tweet tweet!', 'sunnybird');

SELECT * FROM tweets;

+-------------------------------+-----------+---------------------+
| content                       | username  | created_at          |
+-------------------------------+-----------+---------------------+
| This is my first tweet tweet! | sunnybird | 2026-03-28 12:54:36 |
+-------------------------------+-----------+---------------------+
```

<br>