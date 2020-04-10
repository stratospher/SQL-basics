---
description: 'AIM:  Learn to use SQL to access, create, and update data stored in a database'
---

# DAY 1 :GETTING STARTED

We'll be using SQLite.

All data stored in a relational database is of a certain data type. Some of the most common data types are: 

* `INTEGER`, a positive or negative whole number
* `TEXT`, a text string
* `DATE`, the date formatted as YYYY-MM-DD
* `REAL`, a decimal value

## 1.CREATE TABLE

```sql
CREATE TABLE table_name (
   column_1 data_type, 
   column_2 data_type, 
   column_3 data_type
);
```

`CREATE` statements allow us to create a new table in the database.

```sql
CREATE TABLE celebs (
   id INTEGER, 
   name TEXT, 
   age INTEGER
);
```

## 2.INSERT INTO

The `INSERT` statement inserts a new row into a table. 

```sql
INSERT INTO celebs (id, name, age) 
VALUES (1, 'Justin Bieber', 22);
```

## 3.SELECT

`SELECT` statements are used to fetch data from a database. `*` is a special wildcard character that allows you to select every column in a table without having to name each one individually. `SELECT` statements always return a new table called the _result set_.

```sql
SELECT name FROM celebs;
SELECT * FROM celebs;
```

## 4.ALTER TABLE

The `ALTER TABLE` statement adds a new column to a table. You can use this command when you want to add columns to a table. 

```sql
ALTER TABLE celebs 
ADD COLUMN twitter_handle TEXT;
```

1. `ALTER TABLE` is a clause that lets you make the specified changes.   
2. `celebs` is the name of the table that is being changed.   
3. `ADD COLUMN` is a clause that lets you add a new column to a table:   


* `twitter_handle` is the name of the new column being added
* `TEXT` is the data type for the new column

4. `NULL` is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added have `NULL` \(∅\) values for `twitter_handle`.

## 5.UPDATE

The `UPDATE` statement edits a row in a table. You can use the `UPDATE` statement when you want to change existing records

```sql
UPDATE celebs 
SET twitter_handle = '@taylorswift13' 
WHERE id = 4; 
```

1. `UPDATE` is a clause that edits a row in the table.   
2. `celebs` is the name of the table.   
3. `SET` is a clause that indicates the column to edit. 

* `twitter_handle` is the name of the column that is going to be updated
* `@taylorswift13` is the new value that is going to be inserted into the `twitter_handle` column.

4. `WHERE` is a clause that indicates which row\(s\) to update with the new column value. Here the row with a `4` in the `id` column is the row that will have the `twitter_handle` updated to `@taylorswift13`.

## 6.DELETE FROM

The `DELETE FROM` statement deletes one or more rows from a table.

```sql
DELETE FROM celebs 
WHERE twitter_handle IS NULL;
```



1. `DELETE FROM` is a clause that lets you delete rows from a table.
2. `celebs` is the name of the table we want to delete rows from.
3. `WHERE` is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the twitter\_handle column `IS NULL`.
4. `IS NULL` is a condition in SQL that returns true when the value is `NULL` and false otherwise.

## 7. Adding Constraints

_Constraints_ that add information about how a column can be used are invoked after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction. 

```sql
CREATE TABLE celebs (
   id INTEGER PRIMARY KEY, 
   name TEXT UNIQUE,
   date_of_birth TEXT NOT NULL,
   date_of_death TEXT DEFAULT 'Not Applicable'
);
```

### 1.PRIMARY KEY

`PRIMARY KEY` columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a _constraint violation_ which will not allow you to insert the new row.

### 2.UNIQUE

`UNIQUE` columns have a different value for every row. This is similar to `PRIMARY KEY` except a table can have many different `UNIQUE` columns.

### 3.NOT NULL

`NOT NULL` columns must have a value. Attempts to insert a row without a value for a `NOT NULL` column will result in a constraint violation and the new row will not be inserted.

### 4.DEFAULT

`DEFAULT` columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.

