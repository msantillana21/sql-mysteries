**[Check Previous Solution](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/README.md)**

# Finding the mastermind behind SQL Murder game

* Jeremy Bowers (the murderer) said in the interview that he was hired by a woman with a lot of money
* Around 5'5" (65") or 5'7" (67")
* With red hair
* With a Tesla model S
* She attended the SQL Symphony Concert 3 times in December 2017

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/2B.jpg)

* Joining *Drivers license*, *Person*, and *Facebook Event checkin* tables:

```
SELECT height, hair_color, gender, car_make, car_model, name,event_name, date
FROM drivers_license dl
JOIN person p
 ON dl.id = p.license_id
JOIN facebook_event_checkin fb
	ON p.id = fb.person_id
WHERE car_make LIKE 'Tesla%' AND gender = 'female' AND hair_color = 'red'
```

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/12b.jpg)

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/13.jpg)

![fork repository](https://github.com/msantillana21/sql-mysteries/blob/master/My%20Solution/Images/14.jpg)
