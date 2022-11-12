# SQL MURDER MYSTERY GAME

In this project I show my solution to the SQL game and the steps I took to find the person responsible for the "murder".

I used SQLite directly on the game's website: https://mystery.knightlab.com/

## Exploring the Database structure

You start by running this query to find the names of the tables in the database:

```
SELECT name 
FROM sqlite_master
WHERE type = 'table'
```
![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/1.jpg)

## You can also check the schema diagram



![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/2.jpg)



## Using your knowledge of the database schema and SQL to find out who committed the murder

### 1. Gathering the information they tell you about the case:
* By reading the introduction you know that the murder took place at SQL City
* The table that has a City column is the *Crime Scene Report* so you run a query to see the table's data and filter it by City

```
SELECT * 
FROM crime_scene_report
WHERE city = 'SQL City'
```
