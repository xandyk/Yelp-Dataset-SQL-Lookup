# SQL for Data Science
### Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset

![Yelp Dataset ERD](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/hOlYbrgyEeeTsRKxhJ5OZg_517578844a2fd129650492eda3186cd1_YelpERDiagram.png?expiry=1675468800000&hmac=n14sQmWqVFd82eyCOsGC5DDQ01kKwqJ1EkpOuvzwj4c)

### Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:  

- Attribute table   = 10000
- Business table    = 10000
- Category table    = 10000
- Checkin table     = 10000
- elite_years table = 10000
- friend table      = 10000
- hours table       = 10000
- photo table       = 10000
- review table      = 10000
- tip table         = 10000
- user table        = 10000
	
2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

- Business = 10000 records
	- primary key = id
- Hours = 1562 records
	- foreign key = business_id
- Category = 2643 records
	- foreign key = business_id
- Attribute = 1115 records
	- foreign key = business_id
- Review = 10000 records
	- primary key = id 
- Review = 8090 records
	- foreign key = business_id
- Review = 9581 records
	- forein key = user_id
- Checkin = 493 records
	- primary key = business_id
- Photo = 10000 records
	- primary key = id
- Photo = 6493 records
	- forein key = business_id
- Tip = 537 records
	- forein key = user_id
- Tip = 3979 records
	- forein key = business_id
- User = 10000 records
	- primary_key = id
- Friend = 11 records
	- forein key = user_id
- Elite_years = 2780 records
	- forein key = user_id

3. Are there any columns with null values in the Users table? Indicate "yes," or "no." :point_right: No

```
SELECT *
FROM   user
WHERE  id IS NULL
        OR name IS NULL
        OR review_count IS NULL
        OR yelping_since IS NULL
        OR useful IS NULL
        OR funny IS NULL
        OR cool IS NULL
        OR fans IS NULL
        OR average_stars IS NULL
        OR compliment_hot IS NULL
        OR compliment_more IS NULL
        OR compliment_profile IS NULL
        OR compliment_cute IS NULL
        OR compliment_list IS NULL
        OR compliment_note IS NULL
        OR compliment_plain IS NULL
        OR compliment_cool IS NULL
        OR compliment_funny IS NULL
        OR compliment_writer IS NULL
        OR compliment_photos IS NULL 
```

4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:
- Table: Review, Column: Stars
```
  +---------+---------+---------+
  | minimum | maximum | average |
  +---------+---------+---------+
  |       1 |       5 |  3.7082 |
  +---------+---------+---------+
```
	
- Table: Business, Column: Stars
```
  +---------+---------+---------+
  | minimum | maximum | average |
  +---------+---------+---------+
  |       1 |       5 |  3.6549 |
  +---------+---------+---------+
```	
- Table: Tip, Column: Likes
```
  +---------+---------+---------+
  | minimum | maximum | average |
  +---------+---------+---------+
  |       0 |       2 |  0.0144 |
  +---------+---------+---------+
```
- Table: Checkin, Column: Count
```
  +---------+---------+---------+
  | minimum | maximum | average |
  +---------+---------+---------+
  |       1 |      53 |  1.9414 |
  +---------+---------+---------+
```
- Table: User, Column: Review_count
```
  +---------+---------+---------+
  | minimum | maximum | average |
  +---------+---------+---------+
  |       0 |    2000 | 24.2995 |
  +---------+---------+---------+
```
5. List the cities with the most reviews in descending order:
```
SELECT city,
       Sum(review_count) AS reviews
FROM   business
GROUP  BY city
ORDER  BY reviews DESC

+-----------------+---------+
| city            | reviews |
+-----------------+---------+
| Las Vegas       |   82854 |
| Phoenix         |   34503 |
| Toronto         |   24113 |
| Scottsdale      |   20614 |
| Charlotte       |   12523 |
| Henderson       |   10871 |
| Tempe           |   10504 |
| Pittsburgh      |    9798 |
| Montréal        |    9448 |
| Chandler        |    8112 |
| Mesa            |    6875 |
| Gilbert         |    6380 |
| Cleveland       |    5593 |
| Madison         |    5265 |
| Glendale        |    4406 |
| Mississauga     |    3814 |
| Edinburgh       |    2792 |
| Peoria          |    2624 |
| North Las Vegas |    2438 |
| Markham         |    2352 |
| Champaign       |    2029 |
| Stuttgart       |    1849 |
| Surprise        |    1520 |
| Lakewood        |    1465 |
| Goodyear        |    1155 |
+-----------------+---------+
```

6. Find the distribution of star ratings to the business in the following cities:
- Avon
```
SELECT stars,
       Count(stars) AS 'No. of stars'
FROM   business
WHERE  city = 'Avon' 
GROUP  BY stars 

+-------+--------------+
| stars | No. of stars |
+-------+--------------+
|   1.5 |            1 |
|   2.5 |            2 |
|   3.5 |            3 |
|   4.0 |            2 |
|   4.5 |            1 |
|   5.0 |            1 |
+-------+--------------+
```
- Beachwood
```
SELECT stars,
       Count(stars) AS 'No. of stars'
FROM   business
WHERE  city = 'Beachwood'
GROUP  BY stars 

+-------+--------------+
| stars | No. of stars |
+-------+--------------+
|   2.0 |            1 |
|   2.5 |            1 |
|   3.0 |            2 |
|   3.5 |            2 |
|   4.0 |            1 |
|   4.5 |            2 |
|   5.0 |            5 |
+-------+--------------+
```

7. Find the top 3 users based on their total number of reviews:
```
SELECT id AS user,
       review_count
FROM   user
ORDER  BY review_count DESC
LIMIT  3

+------------------------+--------------+
| user                   | review_count |
+------------------------+--------------+
| -G7Zkl1wIWBBmD0KRy_sCw |         2000 |
| -3s52C4zL_DHRK0ULG6qtg |         1629 |
| -8lbUNlXVSoXqaRRiHiSNg |         1339 |
+------------------------+--------------+
```
8. Does posing more reviews correlate with more fans? Please explain your findings and interpretation of the results:

