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



