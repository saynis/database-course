## Lesson 7 — PRIMARY KEY, NOT NULL, UNIQUE, DEFAULT, CHECK
 
### 1. Learning Objectives
Use constraints to make PostgreSQL enforce data rules automatically, instead of relying only on application code.
 
### 2. Why Are We Learning This?
Without constraints, nothing stops two students from sharing an ID, or a required field being left empty. Constraints let the database itself protect your data.
 
### 3. Concept Explanation
 
**PRIMARY KEY** — marks a column as the unique identifier for each row. PostgreSQL automatically enforces uniqueness and disallows empty values.
 
```sql
id INTEGER PRIMARY KEY
```
 
**NOT NULL** — the column can never be left empty.
 
```sql
name VARCHAR(100) NOT NULL
```
 
**UNIQUE** — values in this column must never repeat (but unlike PRIMARY KEY, a table can have several UNIQUE columns, and it can technically allow one NULL, depending on rules — for now just know it enforces "no duplicates").
 
```sql
email VARCHAR(150) UNIQUE
```
 
**DEFAULT** — if no value is given, PostgreSQL automatically fills in a default.
 
```sql
is_active BOOLEAN DEFAULT true
```
 
**CHECK** — enforces a custom rule/condition on the column's value.
 
```sql
age INTEGER CHECK (age >= 0)
```
 
```text
Without constraints:
Two students could accidentally have the same ID,
or someone could insert a student with no name at all.
 
With constraints:
The database itself refuses invalid data —
you don't have to catch every mistake in your application code.
```
 
### 4. Real-World Analogy
Constraints are like the rules at a registration desk: "no two people can have the same ID number" (PRIMARY KEY/UNIQUE), "you must write your name" (NOT NULL), "if you don't pick a plan, you get the free plan" (DEFAULT), "age must be a real, non-negative number" (CHECK).
 
### 5. Visual Explanation
```text
CREATE TABLE students (
  id     INTEGER PRIMARY KEY,     ← must be unique, never empty
  name   VARCHAR(100) NOT NULL,   ← required
  email  VARCHAR(150) UNIQUE,     ← no duplicates allowed
  age    INTEGER CHECK (age >= 0),← must be 0 or more
  is_active BOOLEAN DEFAULT true  ← auto-fills if omitted
);
```
 
### 6. Syntax
```sql
CREATE TABLE table_name (
  column_name data_type PRIMARY KEY,
  column_name data_type NOT NULL,
  column_name data_type UNIQUE,
  column_name data_type DEFAULT value,
  column_name data_type CHECK (condition)
);
```
 
### 7. Example
```sql
CREATE TABLE students (
  id INTEGER PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(150) UNIQUE,
  age INTEGER CHECK (age >= 0),
  is_active BOOLEAN DEFAULT true
);
```
 
### 8. Explain the Example
`id` uniquely identifies each student and can never repeat or be empty. `name` is required. `email` must be unique across all students. `age` is checked to reject negative numbers. `is_active` automatically becomes `true` if not specified during insert.
 
### 9. Common Beginner Mistakes
- Thinking a table can have multiple PRIMARY KEY columns declared separately (a table has exactly one primary key, though it can be made of more than one column together — beyond this course's scope).
- Forgetting that NOT NULL and DEFAULT solve different problems (NOT NULL rejects empty values; DEFAULT fills them in automatically).
- Writing CHECK conditions that are too strict and accidentally reject valid data.
### 10. Mini Practice
Add a PRIMARY KEY to a `books` table's `id` column, and make `title` NOT NULL.
 
### 11. Assignment
Create a `products` table (drop the old one first) with these rules: `id` is the PRIMARY KEY, `product_name` is NOT NULL, `sku` (a product code, VARCHAR(20)) is UNIQUE, `price` uses CHECK to require a value greater than 0, and `is_available` DEFAULTs to `true`.
 
### 12. Assignment Requirements
- All 5 constraints correctly applied as described
- Use `DROP TABLE IF EXISTS products;` before recreating
### 13. Restrictions
No FOREIGN KEY yet (Lesson 13) — this table stands alone.
 
### 14. Expected Result
`\d products` shows all constraints attached to the correct columns.
 
### 15. Concepts Used
```text
Current lesson:
- PRIMARY KEY, NOT NULL, UNIQUE, DEFAULT, CHECK
 
Previous lessons:
- CREATE TABLE, data types (Lessons 5–6)
```
 
---
