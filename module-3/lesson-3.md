## Lesson 10 — Filtering and Sorting: `WHERE`, `ORDER BY`, `LIMIT`
 
### 1. Learning Objectives
Filter rows with `WHERE` and comparison/logical operators, sort results with `ORDER BY`, and limit/paginate results with `LIMIT`/`OFFSET`.
 
### 2. Why Are We Learning This?
Real queries almost never want "everything" — they want "students older than 18" or "the 10 newest orders." This lesson makes SELECT actually useful.
 
### 3. Concept Explanation
 
**WHERE — filtering rows:**
```sql
SELECT * FROM students WHERE age > 18;
```
 
**Comparison operators:** `=`, `!=` (or `<>`), `>`, `<`, `>=`, `<=`
 
**Logical operators — combining conditions:**
```sql
SELECT * FROM students WHERE age > 18 AND is_active = true;
SELECT * FROM students WHERE age < 18 OR is_active = false;
SELECT * FROM students WHERE NOT is_active;
```
 
**IN — match any value in a list:**
```sql
SELECT * FROM students WHERE age IN (19, 20, 21);
```
 
**BETWEEN — a range (inclusive):**
```sql
SELECT * FROM students WHERE age BETWEEN 18 AND 22;
```
 
**LIKE / ILIKE — pattern matching text** (`%` matches any characters, `_` matches one character; `ILIKE` is case-insensitive)
```sql
SELECT * FROM students WHERE name LIKE 'A%';   -- starts with A
SELECT * FROM students WHERE name ILIKE 'a%';  -- same, case-insensitive
```
 
**IS NULL / IS NOT NULL — checking for missing values:**
```sql
SELECT * FROM students WHERE email IS NULL;
SELECT * FROM students WHERE email IS NOT NULL;
```
(You can't use `= NULL` — NULL requires `IS NULL`/`IS NOT NULL`.)
 
**ORDER BY — sorting:**
```sql
SELECT * FROM students ORDER BY age ASC;   -- smallest to largest (default)
SELECT * FROM students ORDER BY age DESC;  -- largest to smallest
```
 
**LIMIT / OFFSET — controlling how many rows, and skipping some:**
```sql
SELECT * FROM students ORDER BY age DESC LIMIT 5;          -- top 5 oldest
SELECT * FROM students ORDER BY age DESC LIMIT 5 OFFSET 5; -- next 5 (pagination)
```
 
### 4. Real-World Analogy
`WHERE` is like telling a librarian "only show me books published after 2020." `ORDER BY` is "now sort them by title." `LIMIT` is "just give me the first 10."
 
### 5. Visual Explanation
```text
students:
id | name  | age
---|-------|----
1  | Ali   | 20
2  | Asha  | 19
3  | Omar  | 22
 
SELECT * FROM students WHERE age > 19 ORDER BY age DESC;
 
Result:
id | name | age
---|------|----
3  | Omar | 22
1  | Ali  | 20
```
 
### 6. Syntax
```sql
SELECT columns FROM table
WHERE condition
ORDER BY column [ASC|DESC]
LIMIT n OFFSET m;
```
 
### 7. Example
```sql
SELECT product_name, price
FROM products
WHERE price < 10 AND is_available = true
ORDER BY price ASC
LIMIT 3;
```
 
### 8. Explain the Example
Finds affordable, available products, cheapest first, and only shows the top 3.
 
### 9. Common Beginner Mistakes
- Using `=` instead of `IS NULL`/`IS NOT NULL` for NULL checks.
- Forgetting that `LIKE` is case-sensitive (use `ILIKE` when case shouldn't matter).
- Writing OFFSET without ORDER BY (results can come back in unpredictable order without sorting).
### 10. Mini Practice
Write a query on `books` that finds all books with a title starting with "The", sorted alphabetically.
 
### 11. Assignment
Using your `products` table, write queries that: (a) find all products under $5, (b) find products where `product_name` contains the word "pen" (any case), (c) list the 3 most expensive available products, (d) find any products with a NULL `sku` if you have one.
 
### 12. Assignment Requirements
- 4 separate SELECT statements matching the 4 requirements above
- Correct use of WHERE, ILIKE, ORDER BY, LIMIT, and IS NULL
### 13. Restrictions
No JOIN, GROUP BY, or subqueries yet.
 
### 14. Expected Result
Four correct, working queries that return exactly the filtered/sorted data described.
 
### 15. Concepts Used
```text
Current lesson:
- WHERE, comparison operators, AND/OR/NOT, IN, BETWEEN, LIKE/ILIKE, IS NULL, ORDER BY, LIMIT, OFFSET
 
Previous lessons:
- SELECT (Lesson 9), INSERT (Lesson 8)
```
 
---
