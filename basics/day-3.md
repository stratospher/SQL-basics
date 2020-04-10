---
description: 'AIM: Calculate + Summarise Data'
---

# DAY 3: AGGREGATES

Calculations performed on multiple rows of a table are called **aggregates**.

## 1.COUNT

`COUNT()` is a function that takes the name of a column as an argument and counts the number of non-empty values in that column.

```sql
SELECT COUNT(*)
FROM table_name;
```

Here, we want to count every row, so we pass `*` as an argument inside the parenthesis.

## 2. SUM

`SUM()` is a function that takes the name of a column as an argument and returns the sum of all the values in that column.

```sql
SELECT SUM(downloads)
FROM fake_apps;
```

## 3. MAX/MIN

The `MAX()` and `MIN()` functions return the highest and lowest values in a column, respectively.

```sql
SELECT MAX(downloads)
FROM fake_apps;
```

## 4. AVERAGE

SQL uses the `AVG()` function to quickly calculate the average value of a particular column.

```sql
SELECT AVG(downloads)
FROM fake_apps;
```

## 5. ROUND

`ROUND()` function takes two arguments inside the parenthesis: 

1. a column name
2. an integer 

It rounds the values in the column to the number of decimal places specified by the integer.

```sql
SELECT ROUND(price, 0)
FROM fake_apps;
```

## 6. GROUP BY

```sql
SELECT year,
   AVG(imdb_rating)
FROM movies
GROUP BY year
ORDER BY year;
```

`GROUP BY` is a clause in SQL that is used with aggregate functions. It is used in collaboration with the `SELECT` statement to arrange identical data into _groups_.

Sometimes, we want to `GROUP BY` a calculation done on a column. For instance, we might want to know how many movies have IMDb ratings that round to 1, 2, 3, 4, 5. We could do this using the following syntax:

```sql
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY ROUND(imdb_rating)
ORDER BY ROUND(imdb_rating);
```

However, this query may be time-consuming to write and more prone to error.

SQL lets us use column reference\(s\) in our `GROUP BY`that will make our lives easier.

* `1` is the first column selected
* `2` is the second column selected
* `3` is the third column selected

and so on.The following query is equivalent to the one above:

```sql
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY 1
ORDER BY 1;
```

## 7. HAVING

In addition to being able to group data using `GROUP BY`, SQL also allows you to filter which groups to include and which to exclude.

We can’t use `WHERE` here because we don’t want to filter the rows; we want to _filter groups_.This is where `HAVING` comes in. `HAVING` is very similar to `WHERE`. In fact, all types of `WHERE` clauses you learned about thus far can be used with `HAVING`.

For instance, imagine that we want to see how many movies of different genres were produced each year, but we only care about years and genres with at least 10 movies.

```sql
SELECT year,
   genre,
   COUNT(name)
FROM movies
GROUP BY 1, 2
HAVING COUNT(name) > 10;
```

* When we want to limit the results of a query based on values of the individual rows, use `WHERE`.
* When we want to limit the results of a query based on an aggregate property, use `HAVING`. 

`HAVING` statement always comes after `GROUP BY`, but before `ORDER BY` and `LIMIT`.

