# Create table, insert into it

Define an `Employees` table, with the following fields:

- `id` - number (automatically increments) and primary key
- `last_name` - text, mandatory
- `first_name` - text, mandatory
- `middle_name` - text, not mandatory
- `age` - number, mandatory
- `current_status` - text, mandatory, defaults to `employed`

```bash
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT,
    last_name VARCHAR(50) NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    middle_name VARCHAR(50),
    age INT NOT NULL,
    current_status VARCHAR(50) NOT NULL DEFAULT 'employed',
    PRIMARY KEY (employee_id)
    );
```

A test insert:

```bash
INSERT INTO employees(first_name, last_name, age)
VALUES('Johann', 'Sebastian', 30);
INSERT INTO employees(first_name, last_name, age)
VALUES('Dora', 'Smith', 58);
```

How the table looks:

```bash
+-------------+-----------+------------+-------------+-----+----------------+
| employee_id | last_name | first_name | middle_name | age | current_status |
+-------------+-----------+------------+-------------+-----+----------------+
|           1 | Sebastian | Johann     | NULL        |  30 | employed       |
|           2 | Smith     | Dora       | NULL        |  58 | employed       |
+-------------+-----------+------------+-------------+-----+----------------+
```