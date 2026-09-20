## Lesson 9 — Reading Data with `SELECT`
 
### 1. Learning Objectives
Retrieve data from a table using `SELECT`, choosing specific columns or all columns.
 
### 2. Why Are We Learning This?
Storing data is only half the story — SELECT is how you actually get it back out and use it.
 
### 3. Concept Explanation
 
```sql
SELECT * FROM students;
```
 
```text
SELECT
↓
I want to retrieve data
 
*
↓
All columns
 
FROM
↓
From which table?
 
students
↓
The students table
```
 
**Selecting specific columns:**
```sql
SELECT name, age FROM students;
```
Only returns the `name` and `age` columns for every row — useful when you don't need everything.
 
### 4. Real-World Analogy
`SELECT *` is like photocopying an entire index card. `SELECT name, age` is like copying just two fields from every card, ignoring the rest.
 
### 5. Visual Explanation
```text
students table:
id | name | email             | age
---|------|-------------------|----
1  | Ali  | ali@example.com   | 20
2  | Asha | asha@example.com  | 19
 
SELECT name, age FROM students;
 
Result:
name | age
-----|----
Ali  | 20
Asha | 19
```
 
### 6. Syntax
```sql
SELECT * FROM table_name;
SELECT column1, column2 FROM table_name;
```
 
### 7. Example
```sql
SELECT product_name, price FROM products;
```
 
### 8. Explain the Example
Returns just the name and price of every product, ignoring `id`, `sku`, and `is_available`.
 
### 9. Common Beginner Mistakes
- Using `SELECT *` in real applications when only a couple of columns are actually needed (fine for learning, wasteful in production).
- Forgetting the semicolon.
- Misspelling a column name (PostgreSQL will show a clear error — read it).
### 10. Mini Practice
Run `SELECT * FROM books;` and then `SELECT title FROM books;`.
 
### 11. Assignment
Write 3 SELECT queries against your `products` table: one that retrieves all columns, one that retrieves only `product_name` and `price`, and one that retrieves only `sku`.
 
### 12. Assignment Requirements
- 3 distinct SELECT statements as described
- Run each and confirm the output columns match what you intended
### 13. Restrictions
No WHERE/ORDER BY/LIMIT yet (Lesson 10) — every SELECT here returns *all rows*.
 
### 14. Expected Result
Three correct, working SELECT statements returning the expected columns for every row in `products`.
 
### 15. Concepts Used
```text
Current lesson:
- SELECT, SELECT *, selecting specific columns, FROM
 
Previous lessons:
- INSERT INTO (Lesson 8), CREATE TABLE (Lesson 5)
```
 
---
