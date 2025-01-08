### MySQL Basics: Rules, Do's, and Don'ts

#### General Rules for Database and Table Naming
1. **Naming Conventions:**
   - Use lowercase letters and underscores (_).
   - Avoid special characters, spaces, or reserved words.
   - Example: Use `student_records` instead of `Student Records` or `student-records`.

2. **Length:**
   - Keep names concise yet descriptive.
   - Avoid overly long or cryptic names.

3. **Consistency:**
   - Use a consistent naming pattern throughout.
   - Example: If you use singular names for tables, apply it uniformly (e.g., `student` instead of `students`).

4. **Prefixes:**
   - Consider adding prefixes for clarity in complex systems.
   - Example: Use `app_users` instead of `users` in a multi-application setup.

---

### Showing Databases
**CODE:**
```sql
SHOW DATABASES;
```
**Do's:**
- Ensure you have the necessary permissions.
- Use `LIKE` to filter databases if needed.
  ```sql
  SHOW DATABASES LIKE 'test%';
  ```
**Don'ts:**
- Don’t rely on case sensitivity for database names unless the operating system enforces it.

---

### Creating Databases
**CODE:**
```sql
CREATE DATABASE school;
```
**Do's:**
- Use meaningful names related to the content.
- Check if the database already exists using `IF NOT EXISTS`:
  ```sql
  CREATE DATABASE IF NOT EXISTS school;
  ```
**Don'ts:**
- Don’t use generic names like `data` or `db`.

---

### Dropping and Using Databases
**CODE:**
```sql
DROP DATABASE school;
USE school;
```
**Do's:**
- Confirm before dropping a database, especially in production.
- Backup data if needed.
**Don'ts:**
- Don’t use `DROP DATABASE` without a backup.
- Don’t drop databases unless absolutely necessary.

---

### Introducing Tables
Tables store data in rows and columns.
- **Syntax:**
  ```sql
  CREATE TABLE table_name (
      column_name datatype constraints
  );
  ```
- Use proper data types and constraints for clarity and efficiency.

---

### Data Types: The Basics
- Common MySQL Data Types:
  - **Numeric:** `INT`, `FLOAT`, `DECIMAL`.
  - **String:** `VARCHAR`, `TEXT`, `CHAR`.
  - **Date/Time:** `DATE`, `DATETIME`, `TIMESTAMP`.
- **Challenge:** Assign appropriate data types for the following:
  - Name
  - Age
  - Date of Birth

**CODE: Basic Datatypes Challenge**
```sql
CREATE TABLE students (
    name VARCHAR(50),
    age INT,
    date_of_birth DATE
);
```

---

### Creating Tables
**CODE:**
```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    role VARCHAR(50),
    salary DECIMAL(10, 2)
);
```
**Do's:**
- Use `PRIMARY KEY` for unique identification.
- Define constraints like `NOT NULL` and `DEFAULT`.
**Don'ts:**
- Don’t leave columns without constraints if they require validation.

---

### How Do We Know It Worked?
**CODE:**
```sql
DESCRIBE employees;
```
Use the `DESCRIBE` statement to view table structure and ensure it matches expectations.

---

### Dropping Tables
**CODE:**
```sql
DROP TABLE employees;
```
**Do's:**
- Confirm dependencies before dropping a table.
**Don'ts:**
- Don’t drop tables without understanding the impact on the database.

---

### Tables Basics Activity
Create a table for tracking books in a library:
- Columns: `id`, `title`, `author`, `published_date`, `available`.

**SOLUTION:**
```sql
CREATE TABLE books (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author VARCHAR(100) NOT NULL,
    published_date DATE,
    available BOOLEAN DEFAULT TRUE
);
```

---

### MySQL Comments
**Single-line comments:**
```sql
-- This is a comment
```
**Multi-line comments:**
```sql
/*
This is a
multi-line comment
*/
```
**Do's:**
- Use comments to explain complex queries.
**Don'ts:**
- Don’t overuse comments to describe obvious code.


---

