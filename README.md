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
# DAY-5

**Why do we need multiple tables in a Database ??**

Multiple tables are needed in a database for several reasons:

1. **Data Normalization**: To prevent data redundancy and ensure data is efficiently distributed across the database.
2. **Data Integrity**: Ensuring consistency and accuracy of data by establishing relationships between tables.
3. **Complex Querying**: Multiple tables allow for complex queries using JOIN operations to fetch related data from different tables.
4. **Security**: Different tables can have different levels of access, improving data security.
5. **Performance**: It's faster and more efficient to search, update, and manage data when it's spread across multiple, smaller tables rather than one large table.

**IMPORTANT LINK**

https://joins.spathon.com/

https://www.kaggle.com/discussions/general/353654

https://www.youtube.com/live/s6xAVqYdmJ4?si=Op4HZZZP5Z7pXNy7

- **JOIN** and **ON** clauses used together will enable you to merge two tables.
- **JOIN**, **ON**, and **AND** clauses will enable you to merge two tables based on multiple columns.
- There is an export button in the SQL editor through which you can download results as a **.csv** file.
- You can assign an abbreviated letter next to the table name to shorten the query length.
- There are multiple kinds of **JOIN** in SQL: **INNER**, **LEFT**, **RIGHT**, **FULL**, and **CROSS JOIN**.
- By default, SQL performs an **INNER JOIN**.
- **LEFT**, **RIGHT**, and **FULL JOINS** are also called **OUTER JOIN**.
- The **UNION** clause will enable you to perform a **FULL JOIN**.

JOIN/INNER JOIN

```sql
SELECT
m.movie_id, title, budget, revenue, currency, unit
FROM movies m
JOIN financials f
ON m.movie_id = f.movie_id;

SELECT
m.movie_id, title, budget, revenue, currency, unit
FROM movies m
INNER JOIN financials f
ON m.movie_id = f.movie_id;
```

LEFT JOIN

```sql
SELECT
m.movie_id, title, budget, revenue, currency, unit
FROM movies m
LEFT JOIN financials f
ON m.movie_id = f.movie_id;
```

RIGHT JOIN

```sql
SELECT
m.movie_id, title, budget, revenue, currency, unit
FROM movies m
RIGHT JOIN financials f
ON m.movie_id = f.movie_id;
```

FULL JOIN

```sql
SELECT
m.movie_id, title, budget, revenue, currency, unit
FROM movies m
LEFT JOIN financials f
ON m.movie_id = f.movie_id

UNION

SELECT
m.movie_id, title, budget, revenue, currency, unit
FROM movies m
RIGHT JOIN financials f
ON m.movie_id = f.movie_id;
```

## QUIZ

1. Generate a report of all Hindi movies sorted by their revenue amount in millions. Print movie name, revenue, currency, and unit

```sql
SELECT * FROM movies;
SELECT * FROM financials;
SELECT * FROM languages;
```

```sql
SELECT title, revenue, currency, unit,
 CASE
    WHEN unit="Thousands" THEN ROUND(revenue/1000,2)
    WHEN unit="Billions" THEN ROUND(revenue*1000,2)
 ELSE revenue
END as revenue_mln
FROM movies m
JOIN financials f ON m.movie_id = f.movie_id
JOIN languages l ON m.language_id=l.language_id
WHERE l.name = "hindi"
ORDER BY revenue_mln DESC
```

# DAY-6 → Sub Queries

- Sub Queries are queries which generate output that will be used as input to the main query.
- Queries that provide a single record, list, or even a table as output can be used as a subquery.

```sql
#this will give the maximum imdb rating
SELECT  MAX(imdb_rating) FROM movies;

#this will give the minimum imdb rating
SELECT  MIN(imdb_rating) FROM movies;

#this will add an age column in the table
SELECT * FROM actors;
SELECT name , YEAR(current_date()) - birth_year AS age
FROM actors;
```

```sql
#TYEP-1 -> returns a single value
SELECT * from movies
WHERE imdb_rating = (SELECT  MAX(imdb_rating) FROM movies);
```

```sql
#TYPE-2 -> returned a list of values
SELECT * from movies
WHERE imdb_rating in ((SELECT  MIN(imdb_rating) FROM movies),
(SELECT  MAX(imdb_rating) FROM movies));
```

```sql
#TYPE-3 -> retures a table (number of rows)
# select all the actors whoose age>70 and age<85

SELECT * FROM
(SELECT name , YEAR(current_date()) - birth_year AS age
FROM actors) as actors_age
WHERE age BETWEEN 70 and 85
```

- **IN, ANY & ALL clauses expect a list as input.**
- **The ANY clause executes the condition for any one of the values on the list that meets the condition, which is the minimum value by default.**
- **The ALL clause executes the condition where all the values on the list meet the condition, which is the maximum value of the list.**

```sql
#select actors who acted in any of the movies (101,110,121)
SELECT * FROM movie_actor;
SELECT * FROM actors;
```

```sql
# these are the actors who actes in the listed movies
SELECT actor_id FROM movie_actor
WHERE movie_id in (101,110,121);
```

```sql
#METHOD-1
SELECT name FROM actors WHERE actor_id in
(SELECT actor_id FROM movie_actor
WHERE movie_id in (101,110,121));
```

```sql
#METHOD-2
SELECT name FROM actors WHERE actor_id = ANY(
SELECT actor_id FROM movie_actor
WHERE movie_id in (101,110,121));
```

**select all the movies whose rating is greater than any of the marval movie rating**

```sql
SELECT * FROM movies;

SELECT imdb_rating FROM movies
WHERE studio = "Marvel Studios";
```

```sql
#METHOD-1
SELECT * FROM movies WHERE imdb_rating > ANY(
SELECT imdb_rating FROM movies
WHERE studio = "Marvel Studios");
```

```sql
#METHOD-2
SELECT * FROM movies WHERE imdb_rating > (
SELECT min(imdb_rating) FROM movies
WHERE studio = "Marvel Studios");
```

```sql
#METHOD-3
SELECT * FROM movies WHERE imdb_rating > SOME (
SELECT (imdb_rating) FROM movies
WHERE studio = "Marvel Studios");
```

**select all the movies whose rating is greater than all of the marval movie rating**

```sql
#Method-1
SELECT * FROM movies WHERE imdb_rating > ALL (
SELECT (imdb_rating) FROM movies
WHERE studio = "Marvel Studios");
```

```sql
#Method-2
SELECT * FROM movies WHERE imdb_rating > (
SELECT max(imdb_rating) FROM movies
WHERE studio = "Marvel Studios");
```

# QUIZ

https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50

### Visits Table:

| visit_id | customer_id |
| --- | --- |
| 1 | 23 |
| 2 | 9 |
| 4 | 30 |
| 5 | 54 |
| 6 | 96 |
| 7 | 54 |
| 8 | 54 |

### Transactions Table:

| transaction_id | visit_id | amount |
| --- | --- | --- |
| 2 | 5 | 310 |
| 3 | 5 | 300 |
| 9 | 5 | 200 |
| 12 | 1 | 910 |
| 13 | 2 | 970 |

### Step 1: LEFT JOIN

We perform a LEFT JOIN on the `Visits` and `Transactions` tables using the `visit_id` column.

### Query:

```sql
SELECT *
FROM Visits V
LEFT JOIN Transactions T
ON V.visit_id = T.visit_id;
```

### Result of LEFT JOIN:

| visit_id | customer_id | transaction_id | amount |
| --- | --- | --- | --- |
| 1 | 23 | 12 | 910 |
| 2 | 9 | 13 | 970 |
| 4 | 30 | NULL | NULL |
| 5 | 54 | 2 | 310 |
| 5 | 54 | 3 | 300 |
| 5 | 54 | 9 | 200 |
| 6 | 96 | NULL | NULL |
| 7 | 54 | NULL | NULL |
| 8 | 54 | NULL | NULL |

### Step 2: WHERE Clause

We filter the results to keep only those rows where `transaction_id` is `NULL`, meaning no transaction was made during those visits.

### Query:

```sql
SELECT *
FROM Visits V
LEFT JOIN Transactions T
ON V.visit_id = T.visit_id
WHERE T.transaction_id IS NULL;
```

### Result after WHERE Clause:

| visit_id | customer_id | transaction_id | amount |
| --- | --- | --- | --- |
| 4 | 30 | NULL | NULL |
| 6 | 96 | NULL | NULL |
| 7 | 54 | NULL | NULL |
| 8 | 54 | NULL | NULL |

### Step 3: GROUP BY Clause

We group the filtered results by `customer_id` to aggregate the number of visits without transactions for each customer.

### Query:

```sql
SELECT
    V.customer_id,
    COUNT(V.visit_id) AS count_no_trans
FROM Visits V
LEFT JOIN Transactions T
ON V.visit_id = T.visit_id
WHERE T.transaction_id IS NULL
GROUP BY V.customer_id;
```

### Result after GROUP BY Clause:

| customer_id | count_no_trans |
| --- | --- |
| 30 | 1 |
| 54 | 2 |
| 96 | 1 |

https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50

`Weather` table:

| id | recordDate | temperature |
| --- | --- | --- |
| 1 | 2015-01-01 | 10 |
| 2 | 2015-01-02 | 25 |
| 3 | 2015-01-03 | 20 |
| 4 | 2015-01-04 | 30 |
- **Join Conditions Evaluation**:
    - For `t1` (2015-01-02, temperature `25`) and `t2` (2015-01-01, temperature `10`): The condition `25 > 10` is true, and `DATEDIFF('2015-01-02', '2015-01-01') = 1` is true, so `id = 2` is included.
    - For `t1` (2015-01-04, temperature `30`) and `t2` (2015-01-03, temperature `20`): The condition `30 > 20` is true, and `DATEDIFF('2015-01-04', '2015-01-03') = 1` is true, so `id = 4` is included.


