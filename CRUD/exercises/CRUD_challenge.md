# CRUD challenge

1. Create new database `shirts_db`
    
    CREATE DATABASE shirts_db;

    USE shirts_db;

2. Create a new table `shirts` with

  `shirt_id`(primarty key)

  `article` (type of shirt)

  `color` 

  `shirt_size`

  `last_worn`

    CREATE TABLE shirts (
      shirt_id INT AUTO_INCREMENT,
      article VARCHAR(50) NOT NULL,
      color VARCHAR(50) NOT NULL,
      shirt_size VARCHAR(20) NOT NULL,
      last_worn INT NOT NULL,
      PRIMARY KEY (shirt_id)
    );


3. Add a provided data:

  ('t-shirt', 'white', 'S', 10),
  ('t-shirt', 'green', 'S', 200),
  ('polo shirt', 'black', 'M', 10),
  ('tank top', 'blue', 'S', 50),
  ('t-shirt', 'pink', 'S', 0),
  ('polo shirt', 'red', 'M', 5),
  ('tank top', 'white', 'S', 200),
  ('tank top', 'blue', 'M', 15)

  INSERT INTO shirts(article, color, shirt_size, last_worn)
  VALUES('t-shirt', 'white', 'S', 10),
    ('t-shirt', 'green', 'S', 200),
    ('polo shirt', 'black', 'M', 10),
    ('tank top', 'blue', 'S', 50),
    ('t-shirt', 'pink', 'S', 0),
    ('polo shirt', 'red', 'M', 5),
    ('tank top', 'white', 'S', 200),
    ('tank top', 'blue', 'M', 15);

4. Add a new shirt

    purple polo shirt, size M, last worn 50 days ago

    INSERT INTO shirts(color, article, shirt_size, last_worn)
    VALUES('purple', 'polo shirt', 'M', 50);

5. Select all shirts, but only print out article and color

    SELECT article, color FROM shirts;

    +------------+--------+
    | article    | color  |
    +------------+--------+
    | t-shirt    | white  |
    | t-shirt    | green  |
    | polo shirt | black  |
    | tank top   | blue   |
    | t-shirt    | pink   |
    | polo shirt | red    |
    | tank top   | white  |
    | tank top   | blue   |
    | polo shirt | purple |
    +------------+--------+

6. Select all **medium** shirts, print out everything except `shirt_id`

    SELECT article, color, shirt_size, last_worn FROM shirts WHERE shirt_size = 'M';

    +------------+--------+------------+-----------+
    | article    | color  | shirt_size | last_worn |
    +------------+--------+------------+-----------+
    | polo shirt | black  | M          |        10 |
    | polo shirt | red    | M          |         5 |
    | tank top   | blue   | M          |        15 |
    | polo shirt | purple | M          |        50 |
    +------------+--------+------------+-----------+

7. Update all polo shirts: change their size to L

    UPDATE shirts SET shirt_size = 'L' WHERE article = 'polo shirt';


8. Update shirt last worn 15 days ago, change `last_worn` to 0

    UPDATE shirts SET last_worn = 0 WHERE last_worn = 15;

9. Update all white shirts: change size to XS and color to off-white

    UPDATE shirts SET shirt_size = 'XS', color = 'off-white' WHERE color = 'white';

10. Delete all old shirts: last worn 200 days ago

    DELETE FROM shirts WHERE last_worn = 200;

11. Delete all tank tops

    DELETE FROM shirts WHERE article = 'tank top';

12. Delete all shirts

    DELETE FROM shirts;

13. Drop the entire `shirts` table

    DROP DATABASE shirts_db;

