## Lesson 6 — PostgreSQL Data Types
 
### 1. Learning Objectives
Choose the correct data type for a given piece of information, from the most common PostgreSQL types.
 
### 2. Why Are We Learning This?
Every column needs a data type — it tells PostgreSQL what kind of value is allowed, and protects your data from mistakes (like storing text where a number belongs).
 
### 3. Concept Explanation
 
We'll cover the most important types — not the entire PostgreSQL type list.
 
**INTEGER** — whole numbers (`20`, `-5`, `1000`)
- Use for: ages, quantities, counts
- Mistake to avoid: using INTEGER for money (rounding errors) — use NUMERIC instead
**BIGINT** — very large whole numbers, beyond INTEGER's range
- Use for: IDs in tables expected to grow into the billions of rows (rare for beginners, but good to know)
**NUMERIC(precision, scale)** — exact decimal numbers
- Use for: money, measurements — anything needing exact decimals
- Example: `NUMERIC(10,2)` allows up to 10 total digits, 2 after the decimal point (`1234.56`)
- Mistake to avoid: forgetting the scale and getting whole numbers only
**VARCHAR(n)** — text with a maximum length
- Use for: names, emails, short text with a known reasonable limit
- Mistake to avoid: setting the limit too small and having real data get rejected
**TEXT** — text with no length limit
- Use for: descriptions, comments, long free-form text
- Mistake to avoid: using TEXT for every string "just in case" when a bounded VARCHAR communicates intent better
**BOOLEAN** — true/false
- Use for: yes/no flags, like `is_active`
- Mistake to avoid: using `0`/`1` integers instead of real booleans
**DATE** — a calendar date, no time (`2026-09-11`)
- Use for: birthdates, enrollment dates
**TIMESTAMP** — a date and time together (`2026-09-11 14:30:00`)
- Use for: "created at", "last login" — anything needing the exact moment
**UUID** — a universally unique identifier (a long random string like `550e8400-e29b-41d4-a716-446655440000`)
- Use for: primary keys in systems where IDs shouldn't be simple sequential numbers (common in larger real-world apps)
- We'll mostly use simple INTEGER IDs in this course for clarity, but you should recognize UUID when you see it.
### 4. Real-World Analogy
```text
Data type   → The kind of box a column is allowed to hold
INTEGER     → A box that only accepts whole numbers
VARCHAR(n)  → A box that only accepts text, up to a certain length
BOOLEAN     → A box that only accepts "yes" or "no"
```
 
### 5. Visual Explanation
```text
students
 
id   INTEGER
name VARCHAR(100)
age  INTEGER
is_active BOOLEAN
enrolled_on DATE
```
 
### 6. Syntax
```sql
column_name INTEGER
column_name VARCHAR(100)
column_name NUMERIC(10,2)
column_name TEXT
column_name BOOLEAN
column_name DATE
column_name TIMESTAMP
```
 
### 7. Example
```sql
CREATE TABLE products (
  id INTEGER,
  product_name VARCHAR(100),
  price NUMERIC(10,2),
  is_available BOOLEAN
);
```
 
### 8. Explain the Example
`price` uses `NUMERIC(10,2)` instead of `INTEGER` because money needs exact decimals. `is_available` uses `BOOLEAN` because it's a true/false flag, not a number or text.
 
### 9. Common Beginner Mistakes
- Using INTEGER or FLOAT for money instead of NUMERIC (causes rounding errors).
- Picking VARCHAR limits that are unrealistically small.
- Using TEXT for everything without thinking about intent.
### 10. Mini Practice
For a `books` table, choose appropriate data types for: `title`, `page_count`, `is_published`, `published_date`.
 
### 11. Assignment
Redesign the `products` table from Lesson 5's assignment, this time choosing the most appropriate data type for each column, and add one new column: `is_available` (BOOLEAN).
 
### 12. Assignment Requirements
- `id` → INTEGER
- `product_name` → VARCHAR with a reasonable limit
- `price` → NUMERIC with sensible precision/scale
- `is_available` → BOOLEAN
- Drop and recreate the table with `DROP TABLE products;` followed by the new `CREATE TABLE`
### 13. Restrictions
No constraints like PRIMARY KEY or NOT NULL yet (Lesson 7).
 
### 14. Expected Result
`\d products` shows all 4 columns with the correct, appropriate data types.
 
### 15. Concepts Used
```text
Current lesson:
- INTEGER, NUMERIC, VARCHAR, TEXT, BOOLEAN, DATE, TIMESTAMP
 
Previous lessons:
- CREATE TABLE (Lesson 5)
```
 
---
