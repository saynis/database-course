## Lesson 13 — Managing Database Structure
 
### 1. Learning Objectives
Change a table's structure after it already exists, using `ALTER TABLE`, and permanently remove tables or columns using `DROP`. Clearly separate commands that change *data* from commands that change *structure*.
 
### 2. Why Are We Learning This?
So far, every table you've built was designed perfectly from the start with `CREATE TABLE`. Real projects are never that tidy — requirements change, and you'll need to add a column, rename one, or remove a table you no longer need, without starting over.
 
### 3. Concept Explanation
 
Every SQL command you've learned so far falls into one of two jobs: changing **data**, or changing **structure**.
 
```text
CREATE → Create something new
 
ALTER  → Change existing structure
 
INSERT → Add data
 
SELECT → Read data
 
UPDATE → Change existing data
 
DELETE → Remove rows
 
DROP   → Remove structure
```
 
The key idea: `UPDATE` changes the data *inside* a table, while `ALTER` changes the *structure* of the table itself.
 
**Adding a column:**
```sql
ALTER TABLE students
ADD COLUMN phone VARCHAR(20);
```
Every existing row gets `NULL` in the new column, unless you also specify a `DEFAULT`.
 
**Removing a column:**
```sql
ALTER TABLE students
DROP COLUMN phone;
```
This permanently deletes the column, and every value stored in it, from every row.
 
**Renaming a column:**
```sql
ALTER TABLE students
RENAME COLUMN phone TO phone_number;
```
 
**Changing a column's data type:**
```sql
ALTER TABLE students
ALTER COLUMN age TYPE BIGINT;
```
PostgreSQL will refuse this if the existing data can't convert safely (e.g. text that doesn't look like a number).
 
**Adding a constraint to an existing column:**
```sql
ALTER TABLE students
ADD CONSTRAINT age_check CHECK (age >= 0);
```
 
**Removing an entire table:**
```sql
DROP TABLE students;
```
This deletes the table structure *and* every row in it — permanently. Unlike `DELETE FROM students;` (which empties the table but keeps it), `DROP TABLE` removes the table itself.
 
```sql
DROP TABLE IF EXISTS students;
```
`IF EXISTS` prevents an error if the table doesn't exist — useful when rebuilding a table from scratch during practice.
 
### 4. Real-World Analogy
`ALTER TABLE` is like renovating a filing cabinet drawer — adding a new labeled slot, renaming a label, or removing a slot entirely — without throwing away the folders already filed correctly in the other slots. `DROP TABLE` is like hauling the entire drawer away.
 
### 5. Visual Explanation
```text
Before:
students (id, name, age)
 
ALTER TABLE students ADD COLUMN email VARCHAR(150);
 
After:
students (id, name, age, email)   ← existing rows now have NULL in email
```
 
### 6. Syntax
```sql
ALTER TABLE table_name ADD COLUMN column_name data_type;
ALTER TABLE table_name DROP COLUMN column_name;
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;
ALTER TABLE table_name ALTER COLUMN column_name TYPE new_data_type;
ALTER TABLE table_name ADD CONSTRAINT constraint_name CHECK (condition);
 
DROP TABLE table_name;
DROP TABLE IF EXISTS table_name;
```
 
### 7. Example
```sql
ALTER TABLE products
ADD COLUMN description TEXT;
 
ALTER TABLE products
RENAME COLUMN product_name TO name;
```
 
### 8. Explain the Example
The first statement adds a new, optional `description` column to every existing product row (filled with `NULL` until updated). The second renames `product_name` to `name` without touching any stored data.
 
### 9. Common Beginner Mistakes
- Confusing `DELETE FROM table;` (empties the table, keeps the structure) with `DROP TABLE table;` (removes the structure entirely, permanently).
- Confusing `UPDATE` (changes data values) with `ALTER TABLE` (changes the table's structure) — they solve completely different problems.
- Running `ALTER COLUMN ... TYPE` on a column whose existing data can't convert cleanly, and being confused by the resulting error.
- Forgetting that `DROP TABLE` cannot be undone — always double-check which table you're targeting.
### 10. Mini Practice
Add a new column called `published_year` (INTEGER) to your `books` table using `ALTER TABLE`.
 
### 11. Assignment
Using your `products` table: (a) add a new column `description` (TEXT), (b) rename `product_name` to `name`, (c) add a CHECK constraint ensuring `price` stays greater than 0 (if it doesn't already have one), (d) write a short note explaining, in your own words, the difference between `UPDATE` and `ALTER TABLE`.
 
### 12. Assignment Requirements
- One `ALTER TABLE ... ADD COLUMN` statement
- One `ALTER TABLE ... RENAME COLUMN` statement
- One `ALTER TABLE ... ADD CONSTRAINT` statement
- A short written explanation distinguishing UPDATE from ALTER TABLE
### 13. Restrictions
No FOREIGN KEY yet (Lesson 15) — keep this lesson's practice to single-table structure changes.
 
### 14. Expected Result
`\d products` shows the renamed column, the new column, and the new constraint, with all existing data intact.
 
### 15. Concepts Used
```text
Current lesson:
- ALTER TABLE (ADD/DROP/RENAME COLUMN, ALTER COLUMN TYPE, ADD CONSTRAINT), DROP TABLE, DROP vs DELETE
 
Previous lessons:
- CREATE TABLE, data types, constraints (Lessons 5–7)
```
 
---
