## Lesson 11 — Updating Data with `UPDATE`
 
### 1. Learning Objectives
Modify existing rows safely using `UPDATE ... SET ... WHERE`.
 
### 2. Why Are We Learning This?
Data changes: a student's email changes, a product's price changes. `UPDATE` is how existing rows get modified — and it is also one of the most dangerous commands if used carelessly.
 
### 3. Concept Explanation
 
```sql
UPDATE students
SET age = 21
WHERE id = 1;
```
 
- `SET` defines which column(s) to change, and their new value(s)
- `WHERE` defines *which rows* get updated
**Updating multiple columns at once:**
```sql
UPDATE students
SET age = 21, is_active = true
WHERE id = 1;
```
 
**⚠️ The most dangerous mistake in SQL:**
```sql
UPDATE students
SET age = 21;
```
This has **no WHERE clause** — it updates the `age` of *every single row in the table*. Always double-check your WHERE clause before running an UPDATE. Many developers run a SELECT with the same WHERE clause first, to confirm exactly which rows will be affected, before running the UPDATE.
 
### 4. Real-World Analogy
`UPDATE` is like pulling one specific index card out of the cabinet and correcting a detail — not throwing out the whole cabinet and starting over. But forgetting WHERE is like grabbing a red pen and rewriting the same field on *every* card in the drawer.
 
### 5. Visual Explanation
```text
Before:
id | name | age
---|------|----
1  | Ali  | 20
 
UPDATE students SET age = 21 WHERE id = 1;
 
After:
id | name | age
---|------|----
1  | Ali  | 21
```
 
### 6. Syntax
```sql
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```
 
### 7. Example
```sql
UPDATE products
SET price = 3.00
WHERE id = 1;
```
 
### 8. Explain the Example
Only the product with `id = 1` has its price changed — every other row is untouched.
 
### 9. Common Beginner Mistakes
- **Forgetting WHERE entirely** (updates every row — always emphasized as the #1 SQL danger).
- Using a WHERE condition that matches more rows than intended.
- Forgetting to check the result with a SELECT afterward.
### 10. Mini Practice
Update one book's title in your `books` table using its `id`.
 
### 11. Assignment
Using your `products` table: (a) update one product's price by its `id`, (b) mark all products under $2 as `is_available = false`, (c) before running each UPDATE, first write the equivalent SELECT to confirm which rows will be affected.
 
### 12. Assignment Requirements
- Two UPDATE statements, each with a correct WHERE clause
- The two matching "preview" SELECT statements, written first
- A one-sentence note on why forgetting WHERE would be dangerous here
### 13. Restrictions
No JOIN-based updates — keep updates on a single table with simple WHERE conditions.
 
### 14. Expected Result
Only the intended rows change; a follow-up SELECT confirms the rest of the table is untouched.
 
### 15. Concepts Used
```text
Current lesson:
- UPDATE, SET, WHERE (in an UPDATE), the danger of missing WHERE
 
Previous lessons:
- SELECT, WHERE, comparison operators (Lessons 9–10)
```
 
---
