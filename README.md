# SQL Most Asked Query_Solution

## Q1.Write a solution to delete all duplicate emails, keeping only one unique email with the smallest id.

Input: 
Person table:

| id | email            |
| -- | ---------------- |
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |


```sql
DELETE FROM Person p1
USING Person p2
WHERE p1.email = p2.email 
  AND p1.id > p2.id;
```
Output:
| id | email            |
| -- | ---------------- |
| 1  | john@example.com |
| 2  | bob@example.com  |

## Q2. Write a query to list the candidates who possess all of the required skills for the job. Sort the output by candidate ID in ascending order.

| candidate_id |skill | 
| -- | ---------------- |
| 123          | Python    |
| 123	         | Tableau   |
| 123	         | PostgreSQL|
| 234	         | R         |
| 234	         | PowerBI   |  
| 234	         | SQL Server|
| 345	         | Python    |
| 345	         | Tableau   |

```sql
SELECT candidate_id
FROM candidates
WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
GROUP BY candidate_id
HAVING COUNT(skill) = 3
ORDER BY candidate_id ASC;
```
Output:
| candidate_id | 
| -- | 
| 123          |

## Q3. Assume you're given a table Twitter tweet data, write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket.


| tweet_id | user_id | msg | tweet_date |
| :--- | :--- | :--- | :--- |
| 214252 | 111 | Am considering taking Tesla private at $420. Funding secured. | 12/30/2021 00:00:00 |
| 739252 | 111 | Despite the constant negative press covfefe | 01/01/2022 00:00:00 |
| 846402 | 111 | Following @NickSinghTech on Twitter changed my life! | 02/14/2022 00:00:00 |
| 241425 | 254 | If the salary is so competitive why won’t you tell me what it is? | 03/01/2022 00:00:00 |
| 231574 | 148 | I no longer have a manager. I can't be managed | 03/23/2022 00:00:00 |

```sql
WITH user_tweets AS (
  SELECT 
    user_id, 
    COUNT(tweet_id) AS tweet_count
  FROM tweets
  WHERE EXTRACT(YEAR FROM tweet_date) = 2022
  GROUP BY user_id
)
SELECT 
  tweet_count AS tweet_bucket, 
  COUNT(user_id) AS users_num
FROM user_tweets
GROUP BY tweet_count;
```
Output:
| tweet_bucket | users_num |
| :--- | :--- |
| 1 | 2 |
| 2 | 1 |




