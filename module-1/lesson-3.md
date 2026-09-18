## Lesson 3 — Tables, Rows, Columns, and Primary Keys
 
### 1. Learning Objectives
Define table, row, column, record, field, and primary key, and read a simple table diagram fluently.
 
### 2. Why Are We Learning This?
Every single thing we do in PostgreSQL happens inside tables. Before writing any SQL, you need rock-solid intuition for this shape.
 
### 3. Concept Explanation
 
A **relational database** organizes data into **tables**. Each table stores one type of "thing" — like students, or products.
 
```text
STUDENTS
 
id | name  | email
---|-------|--------------------
1  | Ali   | ali@example.com
2  | Asha  | asha@example.com
```
 
- **Table** — the whole grid (like `students`)
- **Column** — one type of information (`id`, `name`, `email`) — also called a **field**
- **Row** — one single record (one student) — also called a **record**
- **Value** — one specific piece of data inside a cell (`"Ali"`)
**Primary Key**
Every table needs a way to uniquely identify each row. That's the **primary key** — a column (often `id`) guaranteed to be unique for every row, and never empty. No two students can share the same `id`.
 
**Relationships (preview only)**
Later, we'll connect tables to each other (e.g. connecting `students` to `sections`). For now, just know: relational databases are called "relational" because tables can relate to one another.
 
### 4. Real-World Analogy
```text
Table          → A spreadsheet
Column         → A type of information (like a spreadsheet header)
Row            → One record (one line of the spreadsheet)
Primary Key    → A unique ID card number — no two people share one
```
 
### 5. Visual Explanation
```text
        column      column     column
          ↓            ↓          ↓
        id  |        name  |    email
        ----+---------------+------------------
row →    1  |        Ali    |  ali@example.com
row →    2  |        Asha   |  asha@example.com
```
 
### 6. Syntax
No SQL yet — we introduce `CREATE TABLE` in Lesson 4.
 
### 7. Example
```text
PRODUCTS
 
id | product_name  | price
---|---------------|-------
1  | Notebook      | 2.50
2  | Pen           | 0.75
```
 
### 8. Explain the Example
`id` is the primary key — it uniquely identifies each product. `product_name` and `price` are columns describing each product. Each row is one specific product.
 
### 9. Common Beginner Mistakes
- Confusing "column" and "row" (remember: columns are vertical categories, rows are horizontal records).
- Thinking the primary key has to be called `id` — it doesn't, but `id` is the common convention.
- Forgetting that primary keys must be unique for *every* row, always.
### 10. Mini Practice
Draw (in plain text, like the examples above) a `books` table with columns: `id`, `title`, `author`. Fill in two example rows.
 
### 11. Assignment
Design (on paper/text, no SQL) a table for a `movies` catalog. Include at least 4 columns, one of which is clearly the primary key, and at least 3 rows of realistic sample data.
 
### 12. Assignment Requirements
- Table name
- At least 4 columns, one explicitly marked as the primary key
- At least 3 rows of data
- One sentence explaining why you chose that primary key
### 13. Restrictions
No SQL syntax yet — draw the table using the ASCII/text style shown in this lesson.
 
### 14. Expected Result
A clean, readable table diagram that correctly uses the terms table, column, row, and primary key.
 
### 15. Concepts Used
```text
Current lesson:
- Table, row, column, record, field, value, primary key
 
Previous lessons:
- What is a database, what is a DBMS (Lessons 1–2)
```
