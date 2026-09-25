## Lesson 12 — Deleting Data with `DELETE`
 
### 1. Learning Objectives
Remove rows safely using `DELETE ... WHERE`, and understand how much damage a missing WHERE clause can cause.
 
### 2. Why Are We Learning This?
Sometimes data genuinely needs to be removed. `DELETE` is permanent — this lesson is about doing it carefully.
 
### 3. Concept Explanation
 
```sql
DELETE FROM students
WHERE id = 3;
```
 
**⚠️ Without WHERE:**
```sql
DELETE FROM students;
```
This deletes **every row** in the table (the table itself still exists, but it's now empty). This is one of the most destructive mistakes possible in SQL — always confirm your WHERE clause, and consider running the equivalent SELECT first to see exactly what you're about to delete.
 
**Deleting multiple matching rows:**
```sql
DELETE FROM students
WHERE is_active = false;
```
 
### 4. Real-World Analogy
`DELETE FROM students WHERE id = 3;` is like pulling one specific card out of the cabinet and shredding it. `DELETE FROM students;` (no WHERE) is like shredding every card in the entire drawer.
 
### 5. Visual Explanation
```text
Before:
id | name
---|-----
1  | Ali
2  | Asha
3  | Omar
 
DELETE FROM students WHERE id = 3;
 
After:
id | name
---|-----
1  | Ali
2  | Asha
```
 
### 6. Syntax
```sql
DELETE FROM table_name
WHERE condition;
```
 
### 7. Example
```sql
DELETE FROM products
WHERE is_available = false;
```
 
### 8. Explain the Example
Removes every product currently marked unavailable — and only those rows.
 
### 9. Common Beginner Mistakes
- **Forgetting WHERE and wiping the entire table.**
- Confusing `DELETE FROM table;` with `DROP TABLE table;` (DELETE removes rows; DROP removes the entire table structure).
- Not previewing with SELECT first before an irreversible DELETE.
### 10. Mini Practice
Delete one specific book from your `books` table by its `id`, after first confirming with a SELECT.
 
### 11. Assignment
Using your `products` table: (a) preview with SELECT, then delete any single product by `id`, (b) preview with SELECT, then delete all products where `is_available = false`. Write a short note on what would have happened if you ran `DELETE FROM products;` with no WHERE clause.
 
### 12. Assignment Requirements
- Two preview SELECT statements followed by their matching DELETE statements
- A short written explanation of the danger of a WHERE-less DELETE
### 13. Restrictions
No JOIN-based deletes — single table only.
 
### 14. Expected Result
Only the intended rows are removed; the rest of the table remains intact, confirmed with a follow-up SELECT.
 
### 15. Concepts Used
```text
Current lesson:
- DELETE FROM, WHERE (in a DELETE), the danger of missing WHERE, DELETE vs DROP TABLE
 
Previous lessons:
- UPDATE, WHERE, SELECT (Lessons 9–11)
```
 
---
