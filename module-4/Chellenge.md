# REVIEW CHALLENGE 2 (Lessons 14–17)
 
No new concepts — only what you've already learned.
 
**Scenario:** Extend your `bookstore` database with authors as a separate table.
 
**Task:**
1. Create an `authors` table (`id` PRIMARY KEY, `name` NOT NULL).
2. Add an `author_id` FOREIGN KEY column to your `books` table, referencing `authors(id)`.
3. Insert at least 3 authors, and update your existing books to reference the correct author (or recreate the table if easier).
4. Write an INNER JOIN query showing each book's title alongside its author's name.
5. Add one book with no author assigned (NULL `author_id`), then write a LEFT JOIN showing all books, including that one, 
with the author name showing as NULL where 
missing.
6. How many books does each author have?
7. Which authors have more than 1 book? 
---
