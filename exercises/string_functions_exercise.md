# String functions exercise

1. Reverse and uppercase the following sentence:

    "Što je danas lijep i sunčan dan!"

```sql
SELECT REVERSE(UPPER('Što je danas lijep i sunčan dan!'));

-- !NAD NAČNUS I PEJIL SANAD EJ OTŠ 
```

<br>

2. What does this print out? 

```sql
SELECT
  REPLACE
  (
  CONCAT('I', ' ', 'like', ' ', 'cats'),
  ' ',
  '-'
  );

-- I-like-cats
```

3. Replace spaces in titles with '->' in `books` table. Name the column `title`.

```sql
SELECT REPLACE(title, ' ', '->') AS 'title' FROM books;

    +--------------------------------------------------------------+
    | title                                                        |
    +--------------------------------------------------------------+
    | The->Namesake                                                |
    | Norse->Mythology                                             |
    | American->Gods                                               |
    | Interpreter->of->Maladies                                    |
    | A->Hologram->for->the->King:->A->Novel                       |
    | The->Circle                                                  |
    | The->Amazing->Adventures->of->Kavalier->&->Clay              |
    | Just->Kids                                                   |
    | A->Heartbreaking->Work->of->Staggering->Genius:              |
    | Coraline                                                     |
    | What->We->Talk->About->When->We->Talk->About->Love:->Stories |
    | Where->I'm->Calling->From:->Selected->Stories                |
    | White->Noise                                                 |
    | Cannery->Row                                                 |
    | Oblivion:->Stories                                           |
    | Consider->the->Lobster                                       |
    +--------------------------------------------------------------+
```

<br>

4. Print this out! Don't forget to create aliases!

```sql
SELECT
    author_lname AS 'forwards', REVERSE(author_lname) AS 'backwards'    
FROM
    books;

    +----------------+----------------+
    | forwards       | backwards      |
    +----------------+----------------+
    | Lahiri         | irihaL         |
    | Gaiman         | namiaG         |
    | Gaiman         | namiaG         |
    | Lahiri         | irihaL         |
    | Eggers         | sreggE         |
    | Eggers         | sreggE         |
    | Chabon         | nobahC         |
    | Smith          | htimS          |
    | Eggers         | sreggE         |
    | Gaiman         | namiaG         |
    | Carver         | revraC         |
    | Carver         | revraC         |
    | DeLillo        | olliLeD        |
    | Steinbeck      | kcebnietS      |
    | Foster Wallace | ecallaW retsoF |
    | Foster Wallace | ecallaW retsoF |
    | Smith          | htimS          |
    +----------------+----------------+
```

<br>

5. Print this out the same way, too!

```sql
SELECT UPPER(CONCAT(author_fname, ' ', author_lname)) AS 'full name
in caps' FROM books;

    +----------------------+
    | full name in caps    |
    +----------------------+
    | JHUMPA LAHIRI        |
    | NEIL GAIMAN          |
    | NEIL GAIMAN          |
    | JHUMPA LAHIRI        |
    | DAVE EGGERS          |
    | DAVE EGGERS          |
    | MICHAEL CHABON       |
    | PATTI SMITH          |
    | DAVE EGGERS          |
    | NEIL GAIMAN          |
    | RAYMOND CARVER       |
    | RAYMOND CARVER       |
    | DON DELILLO          |
    | JOHN STEINBECK       |
    | DAVID FOSTER WALLACE |
    | DAVID FOSTER WALLACE |
    | ADAM SMITH           |
    +----------------------+
```

<br>

6. Make this happen! Take `title`, "was released in" + release year of each book and combine them.

```sql
SELECT CONCAT(title, ' was released in ', released_year) AS blurb FROM books;

    +--------------------------------------------------------------------------+
    | blurb                                                                    |
    +--------------------------------------------------------------------------+
    | The Namesake was released in 2003                                        |
    | Norse Mythology was released in 2016                                     |
    | American Gods was released in 2001                                       |
    | Interpreter of Maladies was released in 1996                             |
    | A Hologram for the King: A Novel was released in 2012                    |
    | The Circle was released in 2013                                          |
    | The Amazing Adventures of Kavalier & Clay was released in 2000           |
    | Just Kids was released in 2010                                           |
    | A Heartbreaking Work of Staggering Genius: was released in 2001          |
    | Coraline was released in 2003                                            |
    | What We Talk About When We Talk About Love: Stories was released in 1981 |
    | Where I'm Calling From: Selected Stories was released in 1989            |
    | White Noise was released in 1985                                         |
    | Cannery Row was released in 1945                                         |
    | Oblivion: Stories was released in 2004                                   |
    | Consider the Lobster was released in 2005                                |
    +--------------------------------------------------------------------------+
```

<br>

7. Print the book titles in the length of each book title.

```sql
SELECT title AS 'title', CHAR_LENGTH(title) AS 'character count' FROM books;

    +-----------------------------------------------------+-----------------+
    | title                                               | character count |
    +-----------------------------------------------------+-----------------+
    | The Namesake                                        |              12 |
    | Norse Mythology                                     |              15 |
    | American Gods                                       |              13 |
    | Interpreter of Maladies                             |              23 |
    | A Hologram for the King: A Novel                    |              32 |
    | The Circle                                          |              10 |
    | The Amazing Adventures of Kavalier & Clay           |              41 |
    | Just Kids                                           |               9 |
    | A Heartbreaking Work of Staggering Genius:          |              42 |
    | Coraline                                            |               8 |
    | What We Talk About When We Talk About Love: Stories |              51 |
    | Where I'm Calling From: Selected Stories            |              40 |
    | White Noise                                         |              11 |
    | Cannery Row                                         |              11 |
    | Oblivion: Stories                                   |              17 |
    | Consider the Lobster                                |              20 | 
    +-----------------------------------------------------+-----------------+
```

<br>

8. Print out first 10 characters of all book titles and concatenate it with "...".
    Then print author's with every author's last name + "," + first name.
    Print stock quantity with "in stock" concatenated.

```sql
SELECT
    CONCAT(LEFT(title, 10), '...') AS 'short title',
    CONCAT(author_lname, ', ', author_fname) AS 'author', 
    ONCAT(stock_quantity, ' in stock') AS 'quantity'
FROM
    books;

    +---------------+-------------+--------------+
    | short title   | author      | quantity     |
    +---------------+-------------+--------------+
    | American G... | Gaiman,Neil | 12 in stock  |
    | A Heartbre... | Eggers,Dave | 104 in stock |
    +---------------+-------------+--------------+
```
