## Lesson 8 — Inserting Data with `INSERT INTO`
 
### 1. Learning Objectives
Insert one or multiple rows into a table, with and without specifying every column.
 
### 2. Why Are We Learning This?
Tables are useless empty — this is how real data actually gets in.
 
### 3. Concept Explanation
 
**Basic insert (all columns, in order):**
```sql
INSERT INTO students (id, name, email, age)
VALUES (1, 'Ali', 'ali@example.com', 20);
```
 
**Inserting multiple rows at once:**
```sql
INSERT INTO students (id, name, email, age)
VALUES
  (2, 'Asha', 'asha@example.com', 19),
  (3, 'Omar', 'omar@example.com', 22);
```
 
**Letting DEFAULT fill in a value:**
If a column has a DEFAULT and you don't include it in your column list, PostgreSQL fills it in automatically.
```sql
INSERT INTO students (id, name, email, age)
VALUES (4, 'Layla', 'layla@example.com', 21);
-- is_active will automatically become true
```
 
Always list column names explicitly — it makes your INSERT statements clear and safe even if the table structure changes later.
 
### 4. Real-World Analogy
`INSERT INTO` is like filling out a new index card and filing it into the correct drawer of the cabinet.
 
### 5. Visual Explanation
```text
Before:
students → (empty)
 
INSERT INTO students (id, name, email, age)
VALUES (1, 'Ali', 'ali@example.com', 20);
 
After:
students →
id | name | email            | age
---|------|------------------|----
1  | Ali  | ali@example.com  | 20
```
 
### 6. Syntax
```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```
 
### 7. Example
```sql
INSERT INTO products (id, product_name, sku, price, is_available)
VALUES (1, 'Notebook', 'NB-001', 2.50, true);
```
 
### 8. Explain the Example
This inserts one row into `products`, matching each value to its column in the order listed.
 
### 9. Common Beginner Mistakes
- Mismatching the number/order of values with the number/order of columns.
- Forgetting quotes around text values (`'Ali'`, not `Ali`).
- Violating a constraint (e.g. inserting a duplicate primary key) and being confused by the resulting error.
### 10. Mini Practice
Insert 2 books into your `books` table using a single `INSERT INTO ... VALUES` statement with multiple rows.
 
### 11. Assignment
Insert at least 5 products into your `products` table (from Lesson 7), using realistic sample data. Include at least one insert where you deliberately omit `is_available` so the DEFAULT kicks in.
 
### 12. Assignment Requirements
- At least 5 rows inserted
- At least one multi-row INSERT statement
- At least one row that relies on the DEFAULT for `is_available`
- No constraint violations
### 13. Restrictions
No SELECT/UPDATE/DELETE yet — just get comfortable with INSERT.
 
### 14. Expected Result
`SELECT * FROM products;` (we'll formally learn this next lesson, but you can try it) should show your 5+ rows.
 
### 15. Concepts Used
```text
Current lesson:
- INSERT INTO, VALUES, multi-row insert, relying on DEFAULT
 
Previous lessons:
- CREATE TABLE, constraints (Lessons 5–7)
```
 
---
