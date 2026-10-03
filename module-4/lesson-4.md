## Lesson 17 — Aggregate Functions and `GROUP BY`
 
### 1. Learning Objectives
Answer summary questions about your data using `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `GROUP BY`, and `HAVING`.
 
### 2. Why Are We Learning This?
Real questions are often about totals and averages, not individual rows: "How many students are in each section?" "What's the average price?" Aggregation answers these directly in SQL, instead of pulling all rows and calculating manually in JavaScript.
 
### 3. Concept Explanation
 
**Aggregate functions** summarize many rows into one value:
 
```sql
SELECT COUNT(*) FROM students;         -- how many students total?
SELECT AVG(price) FROM products;       -- average price
SELECT SUM(price) FROM products;       -- total value of all products
SELECT MIN(price) FROM products;       -- cheapest product
SELECT MAX(price) FROM products;       -- most expensive product
```
 
**GROUP BY** — summarize *per group* instead of the whole table:
 
```sql
SELECT section_id, COUNT(*) AS student_count
FROM students
GROUP BY section_id;
```
 
```text
students:
id | name | section_id
---|------|------------
1  | Ali  | 1
2  | Asha | 1
3  | Omar | 2
 
Result:
section_id | student_count
-----------|---------------
1          | 2
2          | 1
```
 
**HAVING** — filters *groups* after aggregation (unlike WHERE, which filters individual rows before grouping):
 
```sql
SELECT section_id, COUNT(*) AS student_count
FROM students
GROUP BY section_id
HAVING COUNT(*) > 1;
```
Only shows sections with more than 1 student.
 
**WHERE vs HAVING:**
```text
WHERE   → filters rows BEFORE grouping
HAVING  → filters groups AFTER aggregation
```
 
### 4. Real-World Analogy
`COUNT`/`SUM`/`AVG` are like a calculator summarizing a stack of index cards. `GROUP BY` is like sorting the cards into separate piles first (one pile per section), then running the calculator on each pile separately.
 
### 5. Visual Explanation
```text
All students → GROUP BY section_id → [pile for section 1] [pile for section 2]
                                              ↓                    ↓
                                        COUNT(*) = 2          COUNT(*) = 1
```
 
### 6. Syntax
```sql
SELECT column, AGG_FUNCTION(column)
FROM table
GROUP BY column
HAVING condition;
```
 
### 7. Example
```sql
SELECT section_id, COUNT(*) AS total_students, AVG(age) AS average_age
FROM students
GROUP BY section_id
HAVING COUNT(*) >= 2
ORDER BY total_students DESC;
```
 
### 8. Explain the Example
Groups students by section, counts them and averages their age per section, keeps only sections with 2+ students, then sorts by student count.
 
### 9. Common Beginner Mistakes
- Selecting a column that isn't in `GROUP BY` and isn't wrapped in an aggregate function (PostgreSQL will error).
- Using `WHERE` when you meant `HAVING` (or vice versa) — remember, WHERE filters rows, HAVING filters groups.
- Forgetting `AS` to name the aggregated column, leading to confusing default column names in results.
### 10. Mini Practice
Write a query counting how many books each author has written, using `GROUP BY author_id`.
 
### 11. Assignment
Using your `bookstore` database: (a) find the total number of books, (b) find the average book price, (c) find how many books each author has, sorted by count descending, (d) find only authors with more than 1 book, using HAVING.
 
### 12. Assignment Requirements
- 4 separate queries matching the 4 requirements
- Correct use of COUNT, AVG, GROUP BY, HAVING
- Correct use of JOIN if you need the author's name (not just `author_id`) in the output
### 13. Restrictions
No subqueries yet (Lesson 18).
 
### 14. Expected Result
Four correct queries producing accurate summary statistics from your data.
 
### 15. Concepts Used
```text
Current lesson:
- COUNT, SUM, AVG, MIN, MAX, GROUP BY, HAVING, WHERE vs HAVING
 
Previous lessons:
- JOIN (Lesson 16), WHERE, ORDER BY (Lesson 10)
```
 
---
