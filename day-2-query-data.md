---
description: 'AIM: Write queries to access data'
---

# DAY 2 : QUERY DATA

## 1. SELECT

```sql
SELECT column1, column2 
FROM table_name;
```

## 2. AS

`AS` is a keyword in SQL that allows you to _rename_ a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes.



Some important things to note:

* Although it’s not always necessary, it’s best practice to surround your aliases with single quotes.
* When using `AS`, the columns are not being renamed in the table. The aliases only appear in the result.

```sql
SELECT name AS 'Titles'
FROM movies;
```

## 3. DISTINCT 

`DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified column\(s\).

```sql
SELECT DISTINCT tools 
FROM inventory;
```

## 4. WHERE

We can restrict our query results using the `WHERE`clause in order to obtain only the information we want.

Following this format, the statement below filters the result set to only include top rated movies \(IMDb ratings greater than 8\):

```sql
SELECT *
FROM movies
WHERE imdb_rating > 8;
```

How does it work?

1. `WHERE` clause filters the result set to only include rows where the following _condition_ is true.
2. `imdb_rating > 8` is the condition. Here, only rows with a value greater than 8 in the `imdb_rating`column will be returned.

## 5. LIKE

`LIKE` can be a useful operator when you want to compare similar values. The `movies` table contains two films with similar titles, ‘Se7en’ and ‘Seven’. 

Q\) select all movies that start with ‘Se’ and end with ‘en’ and have exactly one character in the middle?

```sql
SELECT * 
FROM movies
WHERE name LIKE 'Se_en';
```

* `LIKE` is a special operator used with the `WHERE`clause to search for a specific pattern in a column.
* `name LIKE 'Se_en'` is a condition evaluating the `name` column for a specific pattern.
* `Se_en` represents a pattern with a _wildcard_ character.

The percentage sign `%` is another wildcard character that can be used with `LIKE`.This statement below filters the result set to only include movies with names that begin with the letter ‘A’:

```sql
SELECT * 
FROM movies
WHERE name LIKE 'A%';
```

> > `%` is a wildcard character that matches zero or more missing letters in the pattern. 
> >
> > `LIKE` is not case sensitive.

## 6. IS NULL



Unknown values are indicated by `NULL`.It is not possible to test for `NULL` values with comparison operators, such as `=` and `!=`. Instead, we will have to use these operators:`IS NULL and IS NOT NULL`

```sql
SELECT name
FROM movies 
WHERE imdb_rating IS NOT NULL;
```

## `7. BETWEEN`

The `BETWEEN` operator is used in a `WHERE` clause to filter the result set within a certain _range_. It accepts two values that are either numbers, text or dates.

```sql
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999;
//includes both 1990 and 1999
```

 this statement filters the result set to only include movies with `year`s from 1990 up to, _and including_ 1999.

```sql
SELECT *
FROM movies
WHERE name BETWEEN 'A' AND 'J';
//movies that begin with A,B,C,D,E,F,G,H or I
```

In this statement, `BETWEEN` filters the result set to only include movies with `name`s that begin with the letter ‘A’ up to, _but not including_ ones that begin with ‘J’.However, if a movie has a name of simply ‘J’, it would actually match. This is because `BETWEEN` goes _up to_ the second value — up to ‘J’. So the movie named ‘J’ would be included in the result set but not ‘Jaws’.

## 8. AND

```sql
SELECT * 
FROM movies
WHERE year BETWEEN 1990 AND 1999
   AND genre = 'romance';
```

## 9. OR

```sql
SELECT *
FROM movies
WHERE year > 2014
   OR genre = 'action';
```

##  10. ORDER BY

It is often useful to list the data in our result set in a particular order. We can _sort_ the results using `ORDER BY`, either alphabetically or numerically. Sorting the results often makes the data more useful and easier to analyze.

```sql
SELECT *
FROM movies
ORDER BY name;
```

to sort things in a decreasing order.

```sql
SELECT *
FROM movies
WHERE imdb_rating > 8
ORDER BY year DESC;
```

##  11. LIMIT

`LIMIT` is a clause that lets you specify the maximum number of rows the result set will have. This saves space on our screen and makes our queries run faster. 

```sql
SELECT *
FROM movies
LIMIT 10;
```

`LIMIT` always goes at the very end of the query. Also, it is not supported in all SQL databases.

## 12.  CASE

A `CASE` statement allows us to create different outputs \(usually in the `SELECT` statement\). It is SQL’s way of handling if-then logic.

```sql
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END
FROM movies;
```

* Each `WHEN` tests a condition and the following `THEN` gives us the string if the condition is true.
* The `ELSE` gives us the string if _all_ the above conditions are false.
* The `CASE` statement must end with `END`.

we can rename the column to ‘Review’ using `AS`:

```sql
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END AS 'Review'
FROM movies;
```



