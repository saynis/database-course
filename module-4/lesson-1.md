## Lesson 14 — Why Multiple Tables? Understanding Relationships
 
### 1. Learning Objectives
Explain why data is split across multiple tables instead of one giant table, and recognize one-to-one, one-to-many, and many-to-many relationships.
 
### 2. Why Are We Learning This?
So far every table has stood alone. Real applications need tables that connect to each other — students belong to sections, orders belong to customers. This lesson builds the mental model before we touch any new SQL.
 
### 3. Concept Explanation
 
**Why not put everything in one giant table?**
 
Imagine cramming students and their sections into a single table:
 
```text
id | student_name | section_name | section_teacher
---|--------------|---------------|----------------
1  | Ali          | Section A     | Mr. Yusuf
2  | Asha         | Section A     | Mr. Yusuf
3  | Omar         | Section B     | Ms. Amina
```
 
Notice `Section A` and `Mr. Yusuf` are repeated. If Mr. Yusuf's name is spelled wrong once, you'd have to fix it in every row where it appears — and it's easy to miss one, creating inconsistent data. This is exactly the kind of problem relational databases are built to avoid, by splitting related information into separate tables that reference each other.
 
**Types of relationships:**
 
**One-to-one** — one row in Table A relates to exactly one row in Table B.
```text
students  ↔  student_profiles
(each student has exactly one profile)
```
 
**One-to-many** — one row in Table A can relate to many rows in Table B.
```text
sections
    ↓
belongs to (many students, one section)
    ↓
students
```
```text
sections table          students table
id | name               id | name  | section_id
---|--------             ---|-------|------------
1  | Section A            1  | Ali   | 1
                          2  | Asha  | 1
                          3  | Omar  | 2
```
 
**Many-to-many** — many rows in Table A can relate to many rows in Table B (usually through a third connecting table).
```text
students  ↔  enrollments  ↔  courses
(a student can take many courses; a course can have many students)
```
 
We'll formally connect these tables using **foreign keys**, starting in the next lesson.
 
### 4. Real-World Analogy
```text
One-to-one    → A person and their passport (one passport per person)
One-to-many   → A teacher and their students (one teacher, many students)
Many-to-many  → Students and courses (many students per course, many courses per student)
```
 
### 5. Visual Explanation
```text
sections (1) ────< students (many)
 
students (many) ────< enrollments >──── courses (many)
```
 
### 6. Syntax
No new SQL yet — this lesson is entirely conceptual.
 
### 7. Example
```text
School:
 
teachers (1) ────< sections (many)
sections (1) ────< students (many)
```
One teacher can lead one section. One section can have many students.
 
### 8. Explain the Example
This shows two chained one-to-many relationships, which is very common in real schema design: teacher → sections → students.
 
### 9. Common Beginner Mistakes
- Assuming everything belongs in one big table "to keep it simple" (this actually creates more problems, as shown above).
- Confusing one-to-many with many-to-many (ask: "can the *reverse* also be many?" — if yes, it's many-to-many).
### 10. Mini Practice
Identify the relationship type: a `library` has many `books`, but each `book` belongs to exactly one `library`. One-to-one, one-to-many, or many-to-many?
 
### 11. Assignment
For a small gym app, describe (in plain text, no SQL) the relationship between `trainers` and `members`, and between `members` and `classes` (where a member can attend many classes, and a class can have many members). Identify each relationship type and explain why.
 
### 12. Assignment Requirements
- Identify the `trainers`–`members` relationship type
- Identify the `members`–`classes` relationship type
- One sentence justifying each answer
### 13. Restrictions
No SQL — conceptual only. FOREIGN KEY syntax comes in the next lesson.
 
### 14. Expected Result
Correct identification of one-to-many vs many-to-many, with clear reasoning.
 
### 15. Concepts Used
```text
Current lesson:
- Why multiple tables, one-to-one, one-to-many, many-to-many
 
Previous lessons:
- Tables, rows, columns, primary keys (Lesson 3)
```
 
---
 
