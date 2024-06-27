# -----------------SQL Daily  Learnings------------------
# 
# 
#                    Part-1 :- Data Retrival -> single table
# 😃Day-1

![Screenshot 2024-06-27 125637](https://github.com/gaurav0973/MySQL-/assets/151557489/baabcb47-f38f-4ab3-92d9-0c1d893f081c)

- With the help of the **USE** function, you can indicate the query to use a particular database, especially when there are multiple databases.
- **SELECT, FROM, and WHERE** are the basic SQL functions.
- **‘*’** means all columns. Using ‘*’ after the SELECT query will select all columns of a database.

```sql
SELECT * FROM movies;
SELECT industry, title  FROM movies
```

- The **COUNT** function will provide the numerical count of rows.

```sql
SELECT count(*) FROM movies;
SELECT count(*) FROM movies WHERE industry="bollywood";
```

- The **DISTINCT** function will help you see the unique values present in a given column.

```sql
SELECT DISTINCT industry FROM movies;
```

- **‘%’** is a wild card search.
- Use the **LIKE** function and ‘%’ to filter the search on a text value.

```sql
SELECT * FROM movies WHERE title LIKE "%THOR%";
```

***IMDB search for the movie filter having thor title somewhere***

- Finding the null value in the column

```sql
SELECT * FROM movies WHERE studio="";
```

## QUIZ

Print all movie titles and release year for all Marvel Studios movies

```sql
SELECT title, release_year FROM movies where studio="Marvel Studios";
```

Print all movies that have Avenger in their name.

```sql
SELECT * FROM movies where title LIKE "%Avenger%";
```

Print the year when the movie "The Godfather" was released.

```sql
SELECT release_year FROM movies where title="The Godfather";
```

 Print all distinct movie studios in the Bollywood industry.

```sql
SELECT distinct studio FROM movies WHERE industry="Bollywood";
```

# 😃DAY-2

![Screenshot 2024-06-27 125637](https://github.com/gaurav0973/MySQL-/assets/151557489/baabcb47-f38f-4ab3-92d9-0c1d893f081c)

- **<, >, <=, >=** are the basic numerical operators used in SQL

```sql
SELECT * FROM movies WHERE imdb_rating>=9;
SELECT * FROM movies WHERE imdb_rating<9;
```

- You can also use **AND, OR, BETWEEN, IN** to perform numerical queries.

```sql
# AND --> BETWEEN
SELECT * FROM movies WHERE imdb_rating>=8.5 AND imdb_rating<=9;
SELECT * FROM movies WHERE imdb_rating BETWEEN 8.5 AND 9;

# OR --> IN
SELECT * FROM movies WHERE release_year=2022 OR release_year=2017;
SELECT * FROM movies WHERE release_year IN (2022,2017);
```

- You can sort the table by using the **ORDER BY** clause.

```sql
SELECT * FROM movies WHERE industry="bollywood"
ORDER BY imdb_rating;
```

- By default, it sorts the data in ascending order, but you can specify the sort order.

```sql
SELECT * FROM movies WHERE industry="bollywood"
ORDER BY imdb_rating ASC;

SELECT * FROM movies WHERE industry="bollywood"
ORDER BY imdb_rating DESC;
```

- The **LIMIT** clause can be used to fetch the top ‘N’ or bottom ‘N’ amount of records. ‘N’ can be any numerical value.

```sql
SELECT * FROM movies WHERE industry="bollywood"
ORDER BY imdb_rating DESC LIMIT 5;
```

- The **OFFSET** clause will help you to skip a certain number of rows in your final result.

```sql
SELECT * FROM movies WHERE industry="hollywood"
ORDER BY imdb_rating DESC LIMIT 5 OFFSET 3;
```

- NULL value and other related operations

```sql
SELECT * FROM movies WHERE imdb_rating IS NULL;
SELECT * FROM movies WHERE imdb_rating IS NOT NULL;
```

## QUIZ

Print all movies in the order of their release year (latest first)

```sql
select * from movies order by release_year desc
```

All movies released in the year 2022

```sql
select * from movies where release_year=2022
```

All the movies released after 2020

```sql
select * from movies where release_year>2020
```

All movies after the year 2020 that have more than 8 rating

```sql
select * from movies where release_year>2020 and imdb_rating>8
```

Select all movies that are by Marvel studios and Hombale Films

```sql
select * from movies where studio in ("marvel studios", "hombale films")
```

Select all THOR movies by their release year

```sql
select title, release_year 
from movies
where title like '%thor%' 
order by release_year asc
```

Select all movies that are not from Marvel Studios

```sql
select * from movies where studio != "marvel studios"
```

# 😃DAY-3

![Screenshot 2024-06-27 125637](https://github.com/gaurav0973/MySQL-/assets/151557489/baabcb47-f38f-4ab3-92d9-0c1d893f081c)

- Knowing **Summary Analytics** in SQL will enable you to perform **AD HOC Analysis**, which is an important business use case.
- **MAX, MIN, and AVG** are the common summary analytics functions of SQL.

```sql
SELECT COUNT(*) FROM movies WHERE industry="hollywood";
SELECT MAX(imdb_rating) FROM movies WHERE industry="bollywood";
SELECT MIN(imdb_rating) FROM movies WHERE industry="bollywood";
SELECT AVG(imdb_rating) FROM movies WHERE industry="bollywood";
```

- You can define a custom column header name by using the **‘AS’** clause.

```sql
SELECT AVG(imdb_rating) AS avg_rating
FROM movies WHERE industry="bollywood";
SELECT ROUND(AVG(imdb_rating),2) AS avg_rating
FROM movies WHERE industry="bollywood";

SELECT 
	MIN(imdb_rating) as min_rating,
    MAX(imdb_rating) as max_rating,
	ROUND(AVG(imdb_rating),2) AS avg_rating
FROM movies WHERE industry="bollywood";

```

- The **GROUP BY** clause will help you create a summary of metrics such as average, count, etc., for selected column(s).

```sql
SELECT industry, COUNT(*) as cnt
FROM movies
GROUP BY industry;

SELECT studio, COUNT(*) as cnt
FROM movies
GROUP BY studio;

SELECT studio, COUNT(*) as cnt
FROM movies
GROUP BY studio
ORDER BY cnt DESC;

SELECT
studio,
COUNT(studio) as cnt,
round(AVG(imdb_rating),1) as avg_rating
FROM movies
GROUP BY studio
ORDER BY avg_rating DESC;
```

## QUIZ

How many movies were released between 2015 and 2022

```sql
SELECT
COUNT(title)
FROM movies
WHERE
release_year BETWEEN 2015 AND 2022;
```

Print the max and min movie release year

```sql
SELECT
MAX(release_year) AS max,
MIN(release_year) AS min
FROM movies;
```

Print a year and how many movies were released in that year starting with the latest year

```sql
SELECT
release_year,
COUNT(release_year)  AS cnt
FROM movies
GROUP BY release_year
ORDER BY release_year DESC;
```

# 😃DAY-4

- The order of query execution in SQL is

                      **`FROM → WHERE → GROUP BY → HAVING → ORDER BY`**

- **GROUP BY** and **HAVING** clauses are often used together.
- The column you use in **HAVING** should be present in the **SELECT** clause, whereas **WHERE** can use columns that are not present in the **SELECT** clause as well

```sql
SELECT release_year, COUNT(*) AS movie_count
FROM movies
GROUP BY release_year
HAVING movie_count > 2;
```

![Screenshot 2024-06-27 130316](https://github.com/gaurav0973/MySQL-/assets/151557489/35fbf5d3-53f1-4fc2-98c4-1c2a1be7eb01)

```sql
SELECT * FROM actors;

SELECT YEAR(CURDATE());

SELECT *,
YEAR(CURDATE()) - birth_year as age
FROM actors;
```

- You can derive new columns from the existing columns in a table.
- As a data analyst, **Revenue** and **Profit** are the most common metrics that you will calculate in any industry.

```sql
SELECT *,
(revenue-budget) as profit
FROM financials;
```

![Screenshot 2024-06-27 130437](https://github.com/gaurav0973/MySQL-/assets/151557489/51f8349f-b8e5-46be-80dd-24e3731afe8b)

- Currency conversion and unit conversion are important use cases of SQL
- The IF function is often used in SQL queries.

```sql
SELECT *,
IF(currency='USD', revenue*77, revenue)  AS revenue_inr
FROM financials;
```

- When you have more than two conditions, you need to use the CASE and END functions instead of the IF function

```sql
-- million -> rev;
-- billions -> rev*1000;
-- thousand -> rev/1000;
SELECT distinct unit from financials;

SELECT  **,
	CASE
		WHEN unit="thousands" THEN revenue/1000
		WHEN unit='billions' THEN revenue*1000
		ELSE revenue
	END AS revenue_mln
FROM financials;
```

## QUIZ

- Print profit % for all the movies

```sql
SELECT *,
    (revenue-budget) AS profit,
    (revenue-budget)*100/budget AS profit_percentage
FROM financials;
```


