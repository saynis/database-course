## Lesson 16 — Combining Tables with `JOIN`
 
### 1. Learning Objectives
Write `INNER JOIN` and `LEFT JOIN` queries to combine data across related tables.
 
### 2. Why Are We Learning This?
Foreign keys connect tables structurally — JOINs are how you actually *read* combined data across them in a single query, instead of looking up each table separately.
 
### 3. Concept Explanation
 
```text
students
    +
sections
    ↓
Show student name + section name
```
 
**INNER JOIN** — returns only rows that have a match in *both* tables.
 
```sql
SELECT students.name, sections.name AS section_name
FROM students
INNER JOIN sections ON students.section_id = sections.id;
```
 
```text
students                          sections
id | name | section_id            id | name
---|------|------------            ---|-----------
1  | Ali  | 1                      1  | Section A
2  | Omar | NULL                   2  | Section B
 
INNER JOIN result:
name | section_name
-----|--------------
Ali  | Section A
```
Notice **Omar is missing** — he has no `section_id`, so there's no match, and INNER JOIN excludes him.
 
**LEFT JOIN** — returns *all* rows from the left (first) table, even if there's no match in the right table (filling in NULL where there's no match).
 
```sql
SELECT students.name, sections.name AS section_name
FROM students
LEFT JOIN sections ON students.section_id = sections.id;
```
 
```text
LEFT JOIN result:
name | section_name
-----|--------------
Ali  | Section A
Omar | NULL
```
Now Omar appears, with `NULL` for `section_name`, because LEFT JOIN keeps every row from `students` regardless of a match.
 
**Table aliases** (for shorter, cleaner queries):
```sql
SELECT s.name, sec.name AS section_name
FROM students s
INNER JOIN sections sec ON s.section_id = sec.id;
```
 
### 4. Real-World Analogy
INNER JOIN is like only showing students who *do* have an assigned section. LEFT JOIN is like showing *every* student, and leaving a blank next to any student who hasn't been assigned a section yet.
 
### 5. Visual Explanation
```text
students                sections
   \                       /
    \        JOIN         /
     \                    /
      combined result rows
      (matched on section_id = id)
```
 
### 6. Syntax
```sql
SELECT columns
FROM table_a
INNER JOIN table_b ON table_a.column = table_b.column;
 
SELECT columns
FROM table_a
LEFT JOIN table_b ON table_a.column = table_b.column;
```
 
### 7. Example
```sql
SELECT students.name, sections.name AS section_name
FROM students
INNER JOIN sections ON students.section_id = sections.id
ORDER BY students.name;
```
 
### 8. Explain the Example
This combines `students` and `sections` into one result set, matching each student to their section by `section_id = id`, then sorts alphabetically by student name.
 
### 9. Common Beginner Mistakes
- Forgetting the `ON` condition (PostgreSQL requires it, or you get a confusing, huge "cross join" result).
- Using INNER JOIN when you actually wanted LEFT JOIN (and losing rows without a match).
- Ambiguous column names when both tables have a column with the same name (`name`) — always qualify with the table name or alias.
### 10. Mini Practice
Write an INNER JOIN combining `books` and `libraries` (assuming a `library_id` foreign key), showing book title and library name.
 
### 11. Assignment
Using your `teachers` and `sections` tables from Lesson 15: (a) write an INNER JOIN showing each section's name alongside its teacher's name, (b) add one more section with `teacher_id = NULL`, then write a LEFT JOIN from `sections` to `teachers` and observe how the unassigned section appears.
 
### 12. Assignment Requirements
- One correct INNER JOIN query
- One correct LEFT JOIN query, with a genuinely unmatched row to demonstrate the NULL behavior
- A short note explaining the difference you observed between the two results
### 13. Restrictions
No GROUP BY or aggregation yet (Lesson 17). No subqueries yet (Lesson 18).
 
### 14. Expected Result
INNER JOIN shows only matched rows; LEFT JOIN shows all sections, including the one with no teacher, with `NULL` in its teacher column.
 
### 15. Concepts Used
```text
Current lesson:
- INNER JOIN, LEFT JOIN, table aliases, ON condition
 
Previous lessons:
- FOREIGN KEY, referential integrity (Lesson 15)
- SELECT, WHERE, ORDER BY (Lessons 9–10)
```
 
---
