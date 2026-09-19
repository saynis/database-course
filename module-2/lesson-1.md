## Lesson 5 — SQL Basics: `CREATE DATABASE` and `CREATE TABLE`
 
### 1. Learning Objectives
Write your first real SQL: creating a database and a table with a handful of columns.
 
### 2. Why Are We Learning This?
This is the moment your table diagrams from Lesson 3 become real, queryable structures in PostgreSQL.
 
### 3. Concept Explanation
 
> SQL (Structured Query Language) is the language we use to communicate with relational databases.
 
Every SQL statement ends with a semicolon (`;`). This tells PostgreSQL "this command is complete."
 
**Creating a database:**
```sql
CREATE DATABASE school;
```
This creates a brand-new, empty database named `school`.
 
**Connecting to it (in `psql`):**
```text
\c school
```
 
**Creating a table:**
```sql
CREATE TABLE students (
  id INTEGER,
  name VARCHAR(100),
  age INTEGER
);
```
 
**Naming conventions:**
- Use lowercase, `snake_case` names (`student_name`, not `StudentName`)
- Table names are usually plural (`students`, not `student`)
- Avoid SQL reserved words as names (like `table` or `order`)
### 4. Real-World Analogy
`CREATE DATABASE` is like getting a brand-new empty filing cabinet. `CREATE TABLE` is like adding a labeled drawer to that cabinet, with labeled folders (columns) ready to hold records.
 
### 5. Visual Explanation
```text
CREATE DATABASE school;
       ↓
   [ empty database: school ]
 
CREATE TABLE students (...);
       ↓
   [ empty table: students, with defined columns ]
```
 
### 6. Syntax
```sql
CREATE DATABASE database_name;
 
CREATE TABLE table_name (
  column_name data_type,
  column_name data_type
);
```
 
### 7. Example
```sql
CREATE DATABASE school;
```
```sql
CREATE TABLE students (
  id INTEGER,
  name VARCHAR(100),
  age INTEGER
);
```
 
### 8. Explain the Example
`CREATE DATABASE school;` creates the container. `CREATE TABLE students (...)` creates a table inside whichever database you're currently connected to, with three columns: `id` (a whole number), `name` (text up to 100 characters), and `age` (a whole number).
 
### 9. Common Beginner Mistakes
- Forgetting the semicolon at the end of a statement.
- Running `CREATE TABLE` while connected to the wrong database (always `\c` into the right database first).
- Mismatched parentheses or missing commas between columns.

Create a database called `library`, connect to it, and create a table called `books` with columns `id` (INTEGER) and `title` (VARCHAR(150)).
 
### 11. Assignment
Create a database called `store`. Inside it, create a table called `products` with columns: `id` (INTEGER), `product_name` (VARCHAR(100)), `price` (INTEGER — we'll cover more precise number types next lesson).
 
### 12. Assignment Requirements
- Database named exactly `store`
- Table named exactly `products`
- Exactly the 3 columns listed, in that order
### 13. Restrictions
No constraints (PRIMARY KEY, NOT NULL, etc.) yet — those come in Lesson 7. No data types beyond INTEGER and VARCHAR yet — those come in Lesson 6.
 
### 14. Expected Result
Running `\dt` inside the `store` database should show the `products` table, and `\d products` should show the three correct columns.
 
### 15. Concepts Used
```text
Current lesson:
- CREATE DATABASE, CREATE TABLE, SQL syntax basics, naming conventions
 
Previous lessons:
- psql connection (Lesson 4)
- Table/column concepts (Lesson 3)
```
 
---
