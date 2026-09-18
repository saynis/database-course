# Lesson 4 — What Is PostgreSQL, and Connecting with `psql`
 
### 1. Learning Objectives
Explain what PostgreSQL is (vs. SQL, vs. a database), install/verify PostgreSQL, and connect to it using `psql`.
 
### 2. Why Are We Learning This?
You need a working PostgreSQL setup before you can practice anything else in this course. This lesson also finally nails down the vocabulary that's easy to mix up.
 
### 3. Concept Explanation
 
**Important distinction:**
```text
PostgreSQL  = the DBMS software — manages databases, runs on a server
SQL         = the language we use to talk to PostgreSQL (and other relational DBMSs)
Database    = an organized collection of data
Table       = a structure inside a database that stores records
```
 
PostgreSQL is a **server**. When it's running, it listens for connections and manages one or more **databases**. We talk to it using **SQL** commands, typed through a **client** — the tool we use to send commands to the server.
 
**`psql`** is PostgreSQL's official command-line client. It's how we'll interact with PostgreSQL throughout this course, so that you understand exactly what SQL is doing — not just clicking buttons in a GUI.
 
**Installing PostgreSQL** (brief, platform-dependent):
- Windows/Mac: download the installer from postgresql.org, or use a package manager
- Linux: install via your distro's package manager (e.g. `apt install postgresql`)
After installing, PostgreSQL runs as a background service (the "server").
 
**Connecting:**
```bash
psql -U postgres
```
This opens an interactive prompt where you can type SQL. `-U postgres` means "connect as the user named postgres" (the default admin user PostgreSQL creates during setup).
 
**Basic `psql` commands (not SQL — these are `psql`-specific shortcuts):**
```text
\l          list all databases
\c dbname   connect to a specific database
\dt         list tables in the current database
\d table    describe a table's structure
\q          quit psql
```
 
**Users/roles (beginner level):**
PostgreSQL controls who can connect and what they can do through **roles** (users). For now, know that a role has a username and permissions — we'll touch on this again in database security basics near the end of the course.
 
**GUI option:**
pgAdmin is a popular graphical tool for PostgreSQL. You're welcome to use it to browse your data visually, but every operation we do in this course will be explained in SQL first — the GUI is a bonus, not a requirement.
 
### 4. Real-World Analogy
```text
PostgreSQL server  → A librarian who manages the whole library
Database            → One specific section of the library
psql                → The desk where you hand the librarian your requests
SQL                 → The language you use to make those requests
```
 
### 5. Visual Explanation
```text
You (typing SQL)
      ↓
   psql (client)
      ↓
PostgreSQL server (DBMS)
      ↓
  Databases → Tables → Rows
```
 
### 6. Syntax
```bash
psql -U postgres
```
```sql
\l
\q
```
 
### 7. Example
```bash
$ psql -U postgres
postgres=# \l
postgres=# \q
```
 
### 8. Explain the Example
`psql -U postgres` opens the client and connects as the `postgres` role. `\l` lists existing databases. `\q` exits back to your terminal.
 
### 9. Common Beginner Mistakes
- Confusing PostgreSQL (the server/DBMS) with SQL (the language) — they are not the same thing.
- Forgetting `\q` to exit `psql` and getting stuck in the prompt.
- Trying to run `psql` commands (like `\l`) with a semicolon — `psql` shortcuts don't need one, but SQL statements do.
### 10. Mini Practice
Open `psql`, run `\l` to list your databases, then run `\q` to exit.
 
### 11. Assignment
Install PostgreSQL if you haven't already. Connect using `psql`, run `\l` and take note of what databases already exist by default. Write down, in your own words, the difference between PostgreSQL, SQL, a database, and a table.
 
### 12. Assignment Requirements
- Confirm `psql` opens and connects successfully
- List the default databases you see
- Write a 4-line definition: PostgreSQL / SQL / Database / Table
### 13. Restrictions
No `CREATE TABLE` or data commands yet — this lesson is about setup and vocabulary only.
 
### 14. Expected Result
A working `psql` connection, and a clear written explanation that no longer confuses these four terms.
 
### 15. Concepts Used
```text
Current lesson:
- PostgreSQL vs SQL vs database vs table
- Installing PostgreSQL, psql, basic psql commands
 
Previous lessons:
- Table/row/column/primary key (Lesson 3)
```
 
---