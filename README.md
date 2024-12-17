# Movie Database SQL Queries


## Database Setup

### Step 1: Create the Database and Table

```sql
-- Create a database called MovieDB
CREATE DATABASE MovieDB;

-- Switch to the newly created database
USE MovieDB;

-- Create a Movies table with the specified columns
CREATE TABLE Movies (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    runtime INT,
    genre VARCHAR(50),
    imdb_score DECIMAL(3,1),
    rating VARCHAR(10)
);

Step 2: Insert Initial Movie Data
sql

-- Insert initial movie data into the table

INSERT INTO Movies (title, runtime, genre, imdb_score, rating)
VALUES
    ('Howard the Duck', 110, 'Sci-Fi', 4.6, 'PG'),
    ('Lavalantula', 83, 'Horror', 4.7, 'TV-14'),
    ('Starship Troopers', 129, 'Sci-Fi', 7.2, 'PG-13'),
    ('Waltz With Bashir', 90, 'Documentary', 8.0, 'R'),
    ('Spaceballs', 96, 'Comedy', 7.1, 'PG'),
    ('Monsters Inc.', 92, 'Animation', 8.1, 'G');

Step 3: Add Additional Movies
sql

-- Add two more movies

INSERT INTO Movies (title, runtime, genre, imdb_score, rating)
VALUES
    ('The Matrix', 136, 'Sci-Fi', 8.7, 'R'),
    ('Shrek', 90, 'Animation', 7.9, 'PG');

1. Find All Movies in the Sci-Fi Genre

sql
Copy code
-- Find all movies in the Sci-Fi genre
SELECT * FROM Movies
WHERE genre = 'Sci-Fi';

2. Find Movies Scoring at Least 6.5 on IMDB

sql

SELECT * FROM Movies
WHERE imdb_score >= 6.5;

3. Find G or PG Rated Movies Less Than 100 Minutes Long

SELECT * FROM Movies
WHERE (rating = 'G' OR rating = 'PG') AND runtime < 100;

4. Average Runtime of Movies Scoring Below 7.5, Grouped by Genre

SELECT genre, AVG(runtime) AS avg_runtime
FROM Movies
WHERE imdb_score < 7.5
GROUP BY genre;

5. Update Rating for "Starship Troopers"


UPDATE Movies
SET rating = 'R'
WHERE title = 'Starship Troopers';

6. Show ID and Rating of All Horror and Documentary Movies


SELECT id, rating FROM Movies
WHERE genre IN ('Horror', 'Documentary');

7. Average, Maximum, and Minimum IMDB Scores by Rating


SELECT rating, AVG(imdb_score) AS avg_imdb, MAX(imdb_score) AS max_imdb, MIN(imdb_score) AS min_imdb
FROM Movies
GROUP BY rating;

8. Show Ratings with Multiple Movies Only


SELECT rating, AVG(imdb_score) AS avg_imdb, MAX(imdb_score) AS max_imdb, MIN(imdb_score) AS min_imdb
FROM Movies
GROUP BY rating
HAVING COUNT(*) > 1;

9. Delete Movies Rated 'R'

DELETE FROM Movies
WHERE rating = 'R';
