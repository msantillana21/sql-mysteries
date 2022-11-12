# SQL MURDER MYSTERY GAME

In this project I show my solution to the SQL game and the steps I took to find the person responsible for the "murder".

I used SQLite directly on the game's website: https://mystery.knightlab.com/

## 1. Exploring the Database structure

You start by running this query to find the names of the tables in the database:

```
SELECT name 
  FROM sqlite_master
 where type = 'table'
```
![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/1.jpg)


