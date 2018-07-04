# WEB2040: Databases

This course emphasizes what developers need to know about SQL. Students go through ample practice with nested selects and joins, loading pre-existing datasets into a sql database using the shell, locating and fixing errors in a table, understanding foreign keys and relationships between entities, and creating tables of appropriate data types. An intro to noSQL is also given, with some basic exercises. This course also serves as a Node.JS introduction and AJAX refresher, as students develop CRUD APIs on nodeJS working on a SQL database as well as on noSQL.

## Summary
1. Intro and mariaDB shell, database terms, creating tables and inserting data
2. Select intro, nesting selects
3. Build CRUD application
4. Finish CRUD application, publish to fvi-grad, quiz1.
5. Select Distinct, computed columns, intro to joins
6. DB Theory - normalization, entities, etc. Exam review.
7. Exam 2
8. Intro to Mongo
9. Mongo part 2, introducing mongoose
10. Mongoose Crud application
11. Mongoose Crud application
12. Unit Final Exam

## Grading
Participation/Attendance: 20%
Homework: 10%
In class Projects: 30%
Unit Exams: 40%

## Homework for the Unit
1. Complete the Codecademy SQL course.
2. Complete the TeamTreehouse SQL basics course.
3. Complete the TeamTreehouse "Modifying Data with SQL" course

## Day 1
We do an intro to database concepts and the mariadb shell based on [this presentation](https://docs.google.com/presentation/d/1SKhE9PII6utJ8Wnd6ujx2WRZYdo09y__E72CWBNsFwo/edit?usp=sharing)

We also solve the following exercises in mode analytics:  
1. Select the whole table for the top 100 billboard songs in the tutorial database.
2. Select only the top song for each year and only the year, artist and song title columns

## Day 2
1. Write a query which returns the number of housing units for sale in each region on every month of January since 1983: (table: tutorial.us_housing_units)

2. Show all the monthly housing unit data starting on january of 2014.  

3. Show the monthly sum of all available housing units every month through the financial crisis (2008 and onward). Sum all regions into one, don't split it up by region. Your output table should have year, month, and total housing units.

4. Show the monthly sum of all available housing units every month during years of real estate crises (1979, 1980, 2001, 2008). Sum all regions into one, don't split it up by region.

5. Unguided: Find the total housing units available in the last quarter (per month) of every year since 2003

6. Refactor above query to restrict fields and relabel to year, month (month name) and each region:

7. Get the YEARLY sums of each region since 1987. Display the following columns: year, sum-midwest, sum-northeast, sum-south, sum-west. Make sure results are sorted by year, oldest to newest.

8. Now modify that query from above so you get the yearly AVERAGE rather than sum. Round to the nearest hundredth.

9. Unguided: Get the companies from crunchbase.companies which are located in the los angeles region. Show all columns.

10. Unguided: Build a table where you show the name and total funding raised (value of funding_total_usd column) for all Miami based companies.

11. Now take the above query and sort it from greatest fund raising to lowest.

12. Guided: Get the miami companies and their funding, sorted from most funded to least.

13. In the tutorial.crunchbase_investments table, find all angel investor
activity in Miami. The type of investor is in the funding_round_type column. Show the company name, investor name, and raised amount. Sort it by the raised amount (desc).

14. (Unguided) Use the tutorial.crunchbase_investments table to find the total amount raised by each company in Miami. In your results, show the company name, and the total amount raised. Sort by amount raised (greater to smaller)

15. (Unguided) Use the tutorial.crunchbase_investments table to find the total amount raised in Miami per company category. In your results, show each company category and the amount of money that has been invested into it, ordered descendingly.

16. Cover the concept of nesting Selects.

17. Use the tutorial.crunchbase_investments table to find all the companies nationwide which have raised more money than brightstar

18. Use the tutorial.crunchbase_investments table to find the investors who have invested more money than "Silver Lake Partners"


19. Use sqlzoo.net to practice nested selects and the sum and count sections. Students will complete at their own pace.

## Day 3

Build a CRUD API with node. In the past, we've done a todo app and a fundraising app. We may repeat the old exercises or instructor is free to create a new app if they see fit.

## Day 4

Finish the front end that ties into the CRUD api which was written on the previous day. Teach students how to set up a git remote in their FVI digital ocean space. Have students deploy their applications, run them from the remote server, polish their front ends, make changes to their front ends so that they work by connecting to the fvi-grad remote, and take a [formative assessment](quiz1.md).

**Also make sure to discuss the three servers involved in this application: apache, node, mysql.**


## Day 5
Selecting Distinct records from a table:  
1. (Guided) Using the benn.movie_awards table, figure out how many different types of awards are covered by this data.
  SELECT distinct award_type from benn.movie_awards

2. (Guided) Figure out how many of each award has been given out. Take into account there are multiple rows per award and nomination.  
  ```sql
  SELECT award_type, count(*) as num_awards from
        (SELECT DISTINCT film_name, award_type, category
            from benn.movie_awards
            WHERE winner = 'true') as res1
  group by award_type
  order by num_awards desc
  ```
3. (Unguided) Consider the table with Apple's historical stock prices: tutorial.aapl_historical_stock_price. Write a query which lists the years that this data covers. Use SELECT DISTINCT so that years arent repeated.

4. (Guided) We can use SELEct DISTINCT to identify distinct unique combinations of data. For example, what if we want to select each unique year, month combination from apple's stock price?
  SELECT DISTINCT year, month
  FROM tutorial.aapl_historical_stock_price

5. An estimate for the total amount of money which changed hands in a given day from stock sales can be found by multiplying the **volume** of shares sold times the closing price. Find the total amount of money which changed hands from Apple stock sales since 2008.

6. (Unguided) Back to the benn.movie_awards table, write a query which yields the count of film stars which have won awards. An actor or actress should not be counted multiple times for winning multiple awards.

7. Discuss case statement: You may need a computed value for a column. Example: in the table benn.college_football_players, classify all the players by weight classes:
  * Players above 250lbs are "fluffy"
  * From 201 to 250lbs they are "Swole"
  * Between 175 and 200lbs they are "Athletic"
  * Under 175 they are "Flyweight"

  Show the player's name, weight, and weight class
  SELECT player_name,
       weight,
       CASE WHEN weight > 250 THEN 'over 250'
            WHEN weight > 200 AND weight <= 250 THEN '201-250'
            WHEN weight > 175 AND weight <= 200 THEN '176-200'
            ELSE '175 or under' END AS weight_group
  FROM benn.college_football_players

8. Discuss optimizing the conditions for the query above.  

9. (Guided) Use the benn.college_football_players database to write a query that includes players' names and a column that classifies them into four categories based on height (taller than 6'4 = "giant", between 6'0 and 6'4 is "tall", 5'4 to 5'11 is "normal" and 5'3 and below is "chiquitin".

10. (Unguided) Use the benn.college_football_players database to write a query that includes players' names and a column that classifies them into four categories based on weight:
  * SuperHeavyweight if 235+
  * Heavyweight between 220 and 234
  * Middleweight between 198 and 201-250
  * Welterweight below 198

11. Quick Review:
  * Case statement always goes in the select clause
  * Case must ALWAYS include WHEN, THEN, and END.
  * ELSE is optional
  * WHEN can have multiple conditionals
  * You can have multiple WHEN statements in a select.

12. (Unguided) Use the benn.mky_acquisitions table to figure out what the 100 largest acquirers are. Get the company name and the total amount spent on acquisitions.

13. (Unguided) Use the same above table to categorize acquisitions in sizes: 1 billion is "tres comas club", 500 million and up are "ballers", and the others are "little poor companies". Show Acquirer name, total spent on acquisitions, and computed column

14. Joins: Explain that inner join is the default join and how it behaves; attaches the corresponding row on the joined table to the right hand side of the from table, based on join condition. Rows with no match are left out. Inner join is a mathematical intersection. Show how an inner join works based on this simple example:
  ![Students and Teams](Team.png)
  SELECT * FROM students
  JOIN teams
  ON students.favorite_team = teams.team

  Talk about what this query would produce.

15. General Recipe for Join Syntax:  
  ![Join Recipe](join.png)  

16. Take a look at these two tables: benn.college_football_players and benn.college_football_teams. What if you wanted the player's data plus his team's division and conference in the same table? You need a join. Show player name, position, height, weight, division, conference.  
  SELECT plyrs.full_school_name, plyrs.player_name, plyrs.hometown, plyrs.state,  teamz.division, teamz.conference
  from benn.college_football_players plyrs
  JOIN benn.college_football_teams teamz
  ON plyrs.school_name = teamz.school_name
  limit 450

17. (Unguided) Consider the same two tables as above. For each college football team, show the team name, division, and average height of all team members.

18. [Types of joins](https://www.khanacademy.org/computing/computer-programming/sql/relational-queries-in-sql/p/joining-related-tables)

## Day 6: SQL Theory and Exam Review
1. Download the WHOLE benn.advanced_country_debt_indicators table from mode analytics
2. Create a new DB named countries in your local mysql instance
3. Create a new table named country_debt with an adequate structure for the data in step 1
4. Load the data from step 1 into the table you created on step 3:  
  ![Loading Data from Tables](load-data.png)  
5. Create a query that selects the average gdp growth for each country between the years 1990 and 2000. Show country name and gdp growth.
6. Export your query to a file named NinetiesGDP.csv - use commas to separate the values and quotes to enclose each field  
  ![Writing Data to file](write-data.png)  
7. Create a query that sorts countries by historically highest GDP growth. Show country and GDP growth, and show only 20 results. Take all available yearly data into account. Export this query to a file named top20GDP.csv
8. Which was the country with the largest debt public debt in 1999?
9. Which are the ten countries with the highest historical debt to gdp ratio?
10. Which was the country with the lowest GDP growth in 2008?
11. Sql Unions. Rules for appending data:
  1. Both tables must have the same number of columns
  2. The columns must have the same data types in the same order as the first table
  3. Example:
    ![SQL union](union.png)
12. Write a query that appends the two crunchbase_investments datasets above (including duplicate values). Filter the first dataset to only companies with names that start with the letter "T", and filter the second to companies names starting with "M" (both not case-sensitive). Only include the company_permalink, company_name, and investor_name columns.
13. Hardcoded constants: You can add a hardcoded column by saying something like:
  ```sql
  select 'hardcoded value' as val, name
  from table
  ```
14. You were asked by your boss to produce a query which can help him visualize how company investments change over time. Assume that the tutorial.crunchbase_investments_part1 and part2 tables are from different time periods. Write a query that shows 4 columns. The first indicates **which dataset (part 1 or 2)** the data comes from, the second is the **company permalink**, the third shows company **status**, and the fourth is a **sum of the amount of money** invested into the company. Hint: you will have to use the tutorial.crunchbase_companies table as well as the investments tables (tutorial.crunchbase_investments_part1 and part2).

15. Write a query that shows 4 columns. The first is the company permalink, then company name, status, and number of investors. Make sure all companies are included. Similar to the above problem, but both data sets are lumped together now. Students should attempt to join the companies table to the union of the investments tables.

16. Find out how many investments have been made into companies which are currently closed, acquired, ipo, or operating. These are possible statuses. Ignore companies with no known status.

16. The next query requires you to use the following tables: derek.videogame_weekly_sales_2013_2014, derek.videogame_weekly_sales_2010, derek.videogame_weekly_sales_2011, derek.videogame_weekly_sales_2012. Show the highest grossing video games sold in the spans between 2010 and 2014, adding up xbox and ps3 sales. The tables are derek.videogame_weekly_sales_2013_2014, derek.videogame_global_weekly_sales_2010, derek.videogame_global_weekly_sales_2011, and derek.videogame_global_weekly_sales_2012

### Database theory
[Entities, Attributes, and Relationships](https://www.youtube.com/watch?v=xNJZYX6tpWU)

[Normalization](https://www.youtube.com/watch?v=K7vzLrGCV50&list=PLQ9AAKW8HuJ5m0rmHKL88ZyjOIKejvrj0)

[Entity Types](https://app.pluralsight.com/player?course=relational-database-design&author=hugo-kornelis&name=rel-db-design-02-er-model&clip=2&mode=live)


## Day 7: Exam 2
Sql Exam 2.


## Day 8: [Query and Projection Operators](https://docs.mongodb.com/manual/reference/operator/query/)
=======


1. CRUD in the [mongoshell](https://docs.mongodb.com/manual/reference/operator/query)

2. Find, field selection, gt, lt, exist, querying inside of arrays, in, all, dot notation, where

3. Unguided: Do Mongo Shell exercises on MongoU

## Day 9: Mongoose and Schema Design

1. [Design User Model](scotch.io/tutorials/using-mongoosejs-in-node-js-and-mongodb-applications)

    1. Prototype refresher on codeschool
    2. Explain the concepts of Schemas and Models
  >In mongoose, a schema represents the structure of a particular document, either completely or just a portion of the document. It's a way to express expected properties and values as well as constraints and indexes. A model defines a programming interface for interacting with the database (read, insert, update, etc). So a schema answers "what will the data in this collection look like?" and a model provides functionality like "Are there any records matching this query?" or "Add a new document to the collection".

    3. Review objects and how mongoose has keywords
    4. Setup a Project
    5. Develop Schemas and check the mongo shell

2. [Design Book Schemas](https://www.udemy.com/mongoosejs-essentials)

3. Unguided: [Kitten Schemas ](http://mongoosejs.com/docs/)

## Day 10: [Designing Mongoose REST API](http://adrianmejia.com/blog/2014/10/01/creating-a-restful-api-tutorial-with-nodejs-and-mongodb/):
