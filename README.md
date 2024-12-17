# Movie Database SQL Queries

This document contains a series of SQL queries to interact with a movie database. The database contains information about movies, including their titles, runtime, genre, IMDB score, and rating.

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
Copy code
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
Copy code
-- Add two more movies
INSERT INTO Movies (title, runtime, genre, imdb_score, rating)
VALUES
    ('The Matrix', 136, 'Sci-Fi', 8.7, 'R'),
    ('Shrek', 90, 'Animation', 7.9, 'PG');
SQL Queries
1. Find All Movies in the Sci-Fi Genre
This query returns all movies from the Movies table that belong to the "Sci-Fi" genre.

sql
Copy code
-- Find all movies in the Sci-Fi genre
SELECT * FROM Movies
WHERE genre = 'Sci-Fi';
2. Find Movies Scoring at Least 6.5 on IMDB
This query returns all movies with an IMDB score greater than or equal to 6.5.

sql
Copy code
-- Find all movies with an IMDB score of at least 6.5
SELECT * FROM Movies
WHERE imdb_score >= 6.5;
3. Find G or PG Rated Movies Less Than 100 Minutes Long
This query is aimed at parents looking for shorter movies for their children. It returns all movies rated G or PG with a runtime of less than 100 minutes.

sql
Copy code
-- Find all G or PG rated movies with a runtime of less than 100 minutes
SELECT * FROM Movies
WHERE (rating = 'G' OR rating = 'PG') AND runtime < 100;
4. Average Runtime of Movies Scoring Below 7.5, Grouped by Genre
This query finds the average runtime of movies that scored below 7.5, grouped by genre.

sql
Copy code
-- Find the average runtime of movies scoring below 7.5, grouped by genre
SELECT genre, AVG(runtime) AS avg_runtime
FROM Movies
WHERE imdb_score < 7.5
GROUP BY genre;
5. Update Rating for "Starship Troopers"
There was a data entry mistake. The movie "Starship Troopers" was incorrectly rated "PG-13". This query updates the rating to "R".

sql
Copy code
-- Update the rating of "Starship Troopers" to 'R'
UPDATE Movies
SET rating = 'R'
WHERE title = 'Starship Troopers';
6. Show ID and Rating of All Horror and Documentary Movies
This query returns the id and rating of all movies in the "Horror" and "Documentary" genres.

sql
Copy code
-- Show the ID and rating of all Horror and Documentary movies
SELECT id, rating FROM Movies
WHERE genre IN ('Horror', 'Documentary');
7. Average, Maximum, and Minimum IMDB Scores by Rating
This query calculates the average, maximum, and minimum IMDB scores for each movie rating (G, PG, PG-13, etc.).

sql
Copy code
-- Find the average, maximum, and minimum IMDB scores for each rating
SELECT rating, AVG(imdb_score) AS avg_imdb, MAX(imdb_score) AS max_imdb, MIN(imdb_score) AS min_imdb
FROM Movies
GROUP BY rating;
8. Show Ratings with Multiple Movies Only
This query filters out ratings that only have a single movie associated with them. It uses the HAVING COUNT(*) > 1 clause to show only those ratings with multiple entries.

sql
Copy code
-- Show ratings with multiple movies only
SELECT rating, AVG(imdb_score) AS avg_imdb, MAX(imdb_score) AS max_imdb, MIN(imdb_score) AS min_imdb
FROM Movies
GROUP BY rating
HAVING COUNT(*) > 1;
9. Delete Movies Rated 'R'
For this query, we delete all movies rated "R" to make the movie list more child-friendly.

sql
Copy code
-- Delete all movies with a rating of 'R'
DELETE FROM Movies
WHERE rating = 'R';
