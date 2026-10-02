## Lesson 15 — Connecting Tables with `FOREIGN KEY`
 
### 1. Learning Objectives
Use `FOREIGN KEY` to formally link two tables, and explain referential integrity in your own words.
 
### 2. Why Are We Learning This?
Lesson 14 explained relationships conceptually. Now we make PostgreSQL actually enforce them.
 
### 3. Concept Explanation
 
A **foreign key** is a column in one table that references the primary key of another table.
 
```text
Parent table (referenced)  → sections
Child table (references)   → students
```
 
```sql
CREATE TABLE sections (
  id INTEGER PRIMARY KEY,
  name VARCHAR(50) NOT NULL
);
 
CREATE TABLE students (
  id INTEGER PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  section_id INTEGER REFERENCES sections(id)
);
```
 
`section_id INTEGER REFERENCES sections(id)` means: every value in `students.section_id` must match an existing `id` in the `sections` table (or be NULL, if allowed).
 
**Referential integrity:**
This is the rule that foreign keys enforce — you cannot insert a student with a `section_id` that doesn't exist in `sections`. PostgreSQL rejects it automatically.
 
```sql
INSERT INTO students (id, name, section_id) VALUES (1, 'Ali', 99);
-- ERROR: violates foreign key constraint (no section with id 99 exists)
```
 
**What happens when referenced data changes (beginner-level `ON DELETE`):**
By default, PostgreSQL refuses to delete a row from the parent table (`sections`) if child rows (`students`) still reference it. You can change this behavior:
 
```sql
section_id INTEGER REFERENCES sections(id) ON DELETE CASCADE
```
`ON DELETE CASCADE` means: if a section is deleted, all students in that section are deleted too. Use this carefully — it's powerful and can be destructive. For most beginner scenarios, the default (blocking the delete) is the safer choice.
 
### 4. Real-World Analogy
A foreign key is like writing a section's official ID card number on a student's file — it *points to* a real section that must already exist. You couldn't reference a section that was never created.
 
### 5. Visual Explanation
```text
sections (parent)          students (child)
id | name                  id | name | section_id
---|-----------             ---|------|------------
1  | Section A               1  | Ali  | 1   →  points to sections.id = 1
2  | Section B               2  | Omar | 2   →  points to sections.id = 2
```
 
### 6. Syntax
```sql
CREATE TABLE child_table (
  id INTEGER PRIMARY KEY,
  parent_id INTEGER REFERENCES parent_table(id)
);
```
 
### 7. Example
```sql
CREATE TABLE teachers (
  id INTEGER PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);
 
CREATE TABLE sections (
  id INTEGER PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  teacher_id INTEGER REFERENCES teachers(id)
);
```
 
### 8. Explain the Example
`sections.teacher_id` must match an existing `teachers.id`, formally linking each section to one teacher.
 
### 9. Common Beginner Mistakes
- Creating the child table before the parent table exists (PostgreSQL will error — create parent tables first).
- Forgetting that a foreign key column's data type must match the referenced primary key's data type.
- Trying to delete a referenced parent row without understanding why PostgreSQL blocks it by default.
### 10. Mini Practice
Add a `library_id` foreign key column to a `books` table, referencing a `libraries` table's `id`.
 
### 11. Assignment
Create two tables: `teachers` (`id` PRIMARY KEY, `name` NOT NULL) and `sections` (`id` PRIMARY KEY, `name` NOT NULL, `teacher_id` REFERENCING `teachers(id)`). Insert 2 teachers and 3 sections (correctly linked). Then attempt to insert a section with a `teacher_id` that doesn't exist, and write down the error message you get.
 
### 12. Assignment Requirements
- Both tables created with the FOREIGN KEY correctly applied
- 2 teachers and 3 correctly-linked sections inserted
- One deliberate failed insert, with the error message recorded
### 13. Restrictions
No JOIN queries yet (Lesson 16) — just focus on creating and populating the relationship correctly.
 
### 14. Expected Result
Valid inserts succeed; the invalid `teacher_id` insert is correctly rejected by PostgreSQL.
 
### 15. Concepts Used
```text
Current lesson:
- FOREIGN KEY, REFERENCES, referential integrity, parent/child tables, ON DELETE (conceptual)
 
Previous lessons:
- PRIMARY KEY (Lesson 7), relationships (Lesson 14)
```
 
---
