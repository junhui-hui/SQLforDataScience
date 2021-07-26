# SQLforDataScience
Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset (UC-Davis course on Coursera)

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.



Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:

	SELECT COUNT(*)
	FROM table_name_for_each_sub_part_below(i to xi) ;
	
i. Attribute table = 10000
ii. Business table = 10000
iii. Category table = 10000
iv. Checkin table = 10000
v. elite_years table = 10000
vi. friend table = 10000
vii. hours table = 10000
viii. photo table = 10000
ix. review table = 10000
x. tip table = 10000
xi. user table = 10000
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

	SELECT COUNT(DISTINCT(id))
	FROM business;
i. Business = 10000

	SELECT COUNT(DISTINCT(business_id))
	FROM hours;	
ii. Hours = 1562

	SELECT COUNT(DISTINCT(business_id))
	FROM category;
iii. Category = 2643

	SELECT COUNT(DISTINCT(business_id))
	FROM attribute;
iv. Attribute = 1115

	SELECT COUNT(DISTINCT(id))
	FROM review;
v. Review = 10000

	SELECT COUNT(DISTINCT(business_id))
	FROM checkin;
vi. Checkin = 493

	SELECT COUNT(DISTINCT(business_id))
	FROM photo;
vii. Photo = 6493

	SELECT COUNT(DISTINCT(user_id))
	FROM tip;
viii. Tip = 537

	SELECT COUNT(DISTINCT(id))
	FROM user;
ix. User = 10000

	SELECT COUNT(DISTINCT(user_id))
	FROM friend;
x. Friend = 11

	SELECT COUNT(DISTINCT(user_id))
	FROM elite_years;
xi. Elite_years = 2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: no
	
	
	SQL code used to arrive at answer:
	
	SELECT count(*)
	FROM user
	WHERE id IS NULL OR 
		  name IS NULL OR 
		  review_count IS NULL OR 
		  yelping_since IS NULL OR
		  useful IS NULL OR 
		  funny IS NULL OR 
		  cool IS NULL OR 
		  fans IS NULL OR 
		  average_stars IS NULL OR 
		  compliment_hot IS NULL OR 
		  compliment_more IS NULL OR 
		  compliment_profile IS NULL OR 
		  compliment_cute IS NULL OR 
		  compliment_list IS NULL OR 
		  compliment_note IS NULL OR 
		  compliment_plain IS NULL OR 
		  compliment_cool IS NULL OR 
		  compliment_funny IS NULL OR 
		  compliment_writer IS NULL OR 
		  compliment_photos IS NULL
	
	

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min: 1		max: 5		avg: 3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min: 1.0		max:5.0		avg: 3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min: 0		max: 2		avg: 0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min: 1		max: 53		avg: 1.9414
		
	
	v. Table: User, Column: Review_count
	
		min: 0		max: 2000		avg: 24.2995
		
	SQL code used for this segment:
		SELECT MAX/MIN/AVG(Column_name)
		FROM table_name;

5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	SELECT city, SUM(review_count) AS no_of_reviews
	FROM business
	GROUP BY city
	ORDER BY no_of_reviews DESC;
	
	
	Copy and Paste the Result Below:
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
	(Output limit exceeded, 25 of 362 total rows shown)

	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:
	SELECT stars AS star_rating, SUM(review_count) AS count
	FROM business
	WHERE city = 'Avon'
	GROUP BY stars


Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
	+-------------+-------+
	| star_rating | count |
	+-------------+-------+
	|         1.5 |    10 |
	|         2.5 |     6 |
	|         3.5 |    88 |
	|         4.0 |    21 |
	|         4.5 |    31 |
	|         5.0 |     3 |
	+-------------+-------+

ii. Beachwood

SQL code used to arrive at answer:

	SELECT stars AS star_rating, SUM(review_count) AS count
	FROM business
	WHERE city = 'Beachwood'
	GROUP BY stars

Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
	+-------------+-------+
	| star_rating | count |
	+-------------+-------+
	|         2.0 |     8 |
	|         2.5 |     3 |
	|         3.0 |    11 |
	|         3.5 |     6 |
	|         4.0 |    69 |
	|         4.5 |    17 |
	|         5.0 |    23 |
	+-------------+-------+	


7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
	SELECT name, review_count AS count
	FROM user
	ORDER BY count DESC
	LIMIT 3
		
	Copy and Paste the Result Below:
	+--------+-------+
	| name   | count |
	+--------+-------+
	| Gerald |  2000 |
	| Sara   |  1629 |
	| Yuri   |  1339 |
	+--------+-------+	


8. Does posing more reviews correlate with more fans?
	There is a weak positive correlation between number of reviews posted and the number of fans.
	This can be seen from the many exceptions in this table of 25. People such as Harald, Gerald, William, ROanna, .Hon and Yuri posted over 1000 reviews but still fell short in terms of number of fans as compared to 
	Amy who has only 609 reviews and has the most number of fans. 

	Please explain your findings and interpretation of the results:
	+-----------+--------------+------+---------------------+
	| name      | review_count | fans | yelping_since       |
	+-----------+--------------+------+---------------------+
	| Amy       |          609 |  503 | 2007-07-19 00:00:00 |
	| Mimi      |          968 |  497 | 2011-03-30 00:00:00 |
	| Harald    |         1153 |  311 | 2012-11-27 00:00:00 |
	| Gerald    |         2000 |  253 | 2012-12-16 00:00:00 |
	| Christine |          930 |  173 | 2009-07-08 00:00:00 |
	| Lisa      |          813 |  159 | 2009-10-05 00:00:00 |
	| Cat       |          377 |  133 | 2009-02-05 00:00:00 |
	| William   |         1215 |  126 | 2015-02-19 00:00:00 |
	| Fran      |          862 |  124 | 2012-04-05 00:00:00 |
	| Lissa     |          834 |  120 | 2007-08-14 00:00:00 |
	| Mark      |          861 |  115 | 2009-05-31 00:00:00 |
	| Tiffany   |          408 |  111 | 2008-10-28 00:00:00 |
	| bernice   |          255 |  105 | 2007-08-29 00:00:00 |
	| Roanna    |         1039 |  104 | 2006-03-28 00:00:00 |
	| Angela    |          694 |  101 | 2010-10-01 00:00:00 |
	| .Hon      |         1246 |  101 | 2006-07-19 00:00:00 |
	| Ben       |          307 |   96 | 2007-03-10 00:00:00 |
	| Linda     |          584 |   89 | 2005-08-07 00:00:00 |
	| Christina |          842 |   85 | 2012-10-08 00:00:00 |
	| Jessica   |          220 |   84 | 2009-01-12 00:00:00 |
	| Greg      |          408 |   81 | 2008-02-16 00:00:00 |
	| Nieves    |          178 |   80 | 2013-07-08 00:00:00 |
	| Sui       |          754 |   78 | 2009-09-07 00:00:00 |
	| Yuri      |         1339 |   76 | 2008-01-03 00:00:00 |
	| Nicole    |          161 |   73 | 2009-04-30 00:00:00 |
	+-----------+--------------+------+---------------------+
	(Output limit exceeded, 25 of 10000 total rows shown)

	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: love

	
	SQL code used to arrive at answer:
	
	SELECT COUNT(*)								SELECT COUNT(*)								
	FROM review									FROM review	
	WHERE text LIKE "%love%";					WHERE text LIKE "%hate%";						
																	

	+----------+								+----------+
	| COUNT(*) |								| COUNT(*) |
	+----------+								+----------+
	|     1780 |								|      232 |
	+----------+								+----------+
	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	SELECT
	name,
	fans
	FROM user
	ORDER BY fans DESC
	LIMIT 10;
	
	
	Copy and Paste the Result Below:
	| name      | fans |
	+-----------+------+
	| Amy       |  503 |
	| Mimi      |  497 |
	| Harald    |  311 |
	| Gerald    |  253 |
	| Christine |  173 |
	| Lisa      |  159 |
	| Cat       |  133 |
	| William   |  126 |
	| Fran      |  124 |
	| Lissa     |  120 |
	+-----------+------+
	
	
Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	I picked the city Toronto and the category of my choice is Shopping.
	+------------------------+-------------+----------------------+--------------+-------+--------------+
	| id                     | name        | hours                | review_count | stars | neighborhood |
	+------------------------+-------------+----------------------+--------------+-------+--------------+
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Monday|16:00-2:00    |           26 |   4.5 | High Park    |
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Tuesday|18:00-2:00   |           26 |   4.5 | High Park    |
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Friday|18:00-2:00    |           26 |   4.5 | High Park    |
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Wednesday|18:00-2:00 |           26 |   4.5 | High Park    |
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Thursday|18:00-2:00  |           26 |   4.5 | High Park    |
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Sunday|16:00-2:00    |           26 |   4.5 | High Park    |
	| -n27mJ_jQWGCuIukTvg9Mg | Cabin Fever | Saturday|16:00-2:00  |           26 |   4.5 | High Park    |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Monday|8:00-22:00    |           10 |   2.5 | Roncesvalles |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Tuesday|8:00-22:00   |           10 |   2.5 | Roncesvalles |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Friday|8:00-22:00    |           10 |   2.5 | Roncesvalles |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Wednesday|8:00-22:00 |           10 |   2.5 | Roncesvalles |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Thursday|8:00-22:00  |           10 |   2.5 | Roncesvalles |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Sunday|8:00-22:00    |           10 |   2.5 | Roncesvalles |
	| 1vBwbEnM65zyxiJZTttMJQ | Loblaws     | Saturday|8:00-22:00  |           10 |   2.5 | Roncesvalles |
	+------------------------+-------------+----------------------+--------------+-------+--------------+
i. Do the two groups you chose to analyze have a different distribution of hours?
	Yes the two groups have a different distribution of hours. The one with higher ratings opens in the late afternoon and
	closes past midnight and the one with the lower ratings opens early in the morning and closes before midnight.

ii. Do the two groups you chose to analyze have a different number of reviews?
    Yes, the one with higher rating have more number of reviews than the one with lower rating.     
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
	The neighbourhood of these 2 groups are different. It is possible that people in both neighborhood prefer a food store that
	opens past midnight rather than one that closes before midnight.
SQL code used for analysis:

	SELECT  b.id,
        b.name, 
        h.hours,
        b.review_count,
        b.stars,
        b.neighborhood
	FROM business as b
	INNER JOIN hours as h
	ON b.id == h.business_id
	INNER JOIN category as c
	ON b.id == c.business_id
	WHERE (b.city = 'Toronto'AND c.category = 'Food')
	AND (b.stars BETWEEN 2.0 AND 3.0 OR b.stars BETWEEN 4.0 AND 5.0)
    LIMIT 14

		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1: The businesses that are open have a slightly higher average star rating than the business that are closed.
         
         
ii. Difference 2: The businesses that are open have a higher average number of reviews than the businesses that are closed.
         
         
         
SQL code used for analysis:

	SELECT is_open,
        COUNT(DISTINCT(id)),
        AVG(stars),
        SUM(review_count)/COUNT(DISTINCT(id)) AS avg_no_of_reviews
	FROM business
	GROUP BY is_open
	
	+---------+---------------------+---------------+-------------------+
	| is_open | COUNT(DISTINCT(id)) |    AVG(stars) | avg_no_of_reviews |
	+---------+---------------------+---------------+-------------------+
	|       0 |                1520 | 3.52039473684 |                23 |
	|       1 |                8480 | 3.67900943396 |                31 |
	+---------+---------------------+---------------+-------------------+
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
    Finding whether there is a correlation between captions/labels and number of checkins
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
    I will need the to join the tables of photos and checkins using their common key and extract these data: 1) checkin counts, 2) whether there is caption or labels
                  
iii. Output of your finished dataset:
    +------------------------+-------+----------------------+--------+
	| business_id            | count | caption              | label  |
	+------------------------+-------+----------------------+--------+
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     2 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     2 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| HRIUU2Z4EsZBo59P0I2ZYA |     1 |                      | food   |
	| tZOr1d79vMvUV5XQBmcYdw |     2 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     1 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     2 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     1 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     1 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     1 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     3 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     4 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     3 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     1 | The fountain display | inside |
	| tZOr1d79vMvUV5XQBmcYdw |     1 | The fountain display | inside |
	+------------------------+-------+----------------------+--------+
	(Output limit exceeded, 25 of 508 total rows shown)
         
	From the data above, it can be seen that photos with caption and labels are more likely to have checkin counts
iv. Provide the SQL code you used to create your final dataset:

	SELECT c.business_id,
        c.count,
        p.caption,
        p.label
        FROM checkin c INNER JOIN photo p ON c.business_id = p.business_id;
