# SQL MURDER MYSTERY GAME

In this project I show my solution to the SQL game and the steps I took to find the person responsible for the "murder".

I used SQLite directly on the game's website: https://mystery.knightlab.com/

## VIZ

[You can check my Tableau highlights viz here](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/README3.md)

## Exploring the Database structure

You start by running this query to find the names of the tables in the database:

```
SELECT name 
FROM sqlite_master
WHERE type = 'table'
```
![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/1B.jpg)

## Checking the schema diagram



![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/2B.jpg)



## Using my knowledge of the database schema and SQL to find out who committed the murder

### 1. Gathering the information they tell you about the case:
* By reading the introduction you know that the murder took place in SQL City on Jan.15, 2018 
* The table that has a City column is the *Crime Scene Report*
* There are 1228 entries in this table, so you run a query to see the table's data filtered by City

```
SELECT COUNT(*)
FROM crime_scene_report
```
![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/3c.jpg)


```
SELECT * 
FROM crime_scene_report
WHERE city = 'SQL City'
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/3.jpg)

Looking only at the 'murder' reports and the date (20180115) you can see that there are 2 witnesses:

  *The first witness lives at the last house on "Northwestern Dr".*
  
  *The second witness, named Annabel, lives somewhere on "Franklin Ave".*
  
 ### 2. Creating a query to search the names of the witnesses
 * The table that has names and addresses is the *person* table
 * Since the first witness lives on the last house, you order by descending number to show the last house of that street on the first row
 
 ```
SELECT *
FROM person
WHERE address_street_name = 'Northwestern Dr'
ORDER BY address_number DESC
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/4.jpg)

You get the first name: *Morty Schapiro*

* Then you search for the other witness filtering by name and street name:

 ```
SELECT *
FROM person
WHERE address_street_name = 'Franklin Ave' AND name LIKE 'Annabel%'
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/5.jpg)

You get the second name: *Annabel Miller*

### 3. Querying what the witnesses saw or heard 
 
* Since the interview table only has 2 columns: *person_id* and *transcript*, you filter your witnesses by person_id which is a column in common with the *person* table

 ```
SELECT *
FROM interview
WHERE person_id = 14887 OR person_id = 16371
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/6.jpg)

### 4. Querying the person with the license plate number that includes **H42W**
* Joining the *person* and the *drivers license* tables

 ```
SELECT *
FROM drivers_license dl
JOIN person p
	ON dl.id = p.license_id
WHERE  plate_number LIKE '%H42W%'
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/7b.jpg)

The query finds 3 results, but the first witness said that he saw a **man**, so you narrow down to the first 2: Tushar Chandra or Jeremy Bowers.

### 5. Querying the gym information given by the witnesses

* Selecting the columns that will be more useful
* Joining *get fit now member* and *get fit now check in* tables
* Filtering by membership id containing **48Z**

 ```
SELECT name, membership_status, membership_id, check_in_date
FROM get_fit_now_member gym
JOIN get_fit_now_check_in checkin
	ON gym.id = checkin.membership_id
WHERE membership_id LIKE '%48z%
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/8.jpg)

The person that has a gold membership, checked in on January the 9th as the witnesses said and appeared on the previous license query is **Jeremy Bowers**

### 6. Making your guess 

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/9.jpg)

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/10.jpg)

### 7. Checking Jeremy's interview transcript

 ```
SELECT *
FROM person p
JOIN interview i
 ON p.id = i.person_id
WHERE name = 'Jeremy Bowers'
```
![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/11.jpg)


### 8. Want to find the real villain?

**[See More...](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/README2.md)**

