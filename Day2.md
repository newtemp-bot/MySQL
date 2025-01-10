### MySQL Tables and Constraints

#### Table Definition
A table is a structured set of data stored in rows and columns. Each table has a unique name and is defined using columns with specific data types and constraints.

#### Common Constraints
1. **NOT NULL**: Ensures a column cannot have NULL values.
2. **UNIQUE**: Ensures all values in a column are unique.
3. **PRIMARY KEY**: Combines `NOT NULL` and `UNIQUE` to uniquely identify rows.
4. **FOREIGN KEY**: Links one table to another for referential integrity.
5. **DEFAULT**: Sets a default value for a column if no value is provided.
6. **CHECK**: Ensures all values in a column satisfy a specific condition.
7. **AUTO_INCREMENT**: Automatically generates a unique value for a column.

**How Tables Are Created:**
```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```

**Example Table Creation:**
```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT CHECK (age >= 18),
    department VARCHAR(50) DEFAULT 'General',
);
```
---

### SQL Commands Categorized

#### 1. **DDL (Data Definition Language)**
Commands used to define or modify database structures.
- **CREATE**: Creates a database or table.
- **ALTER**: Modifies table structure.
- **DROP**: Deletes a table or database.
- **TRUNCATE**: Removes all rows from a table.

**Do's:**
- Backup data before using `DROP` or `TRUNCATE`.
- Plan the schema structure carefully.
**Don'ts:**
- Don’t modify tables without understanding dependencies.

#### 2. **DQL (Data Query Language)**
Commands used to retrieve data from the database.
- **SELECT**: Fetches data from tables.

**Do's:**
- Use `WHERE` clauses to filter results.
- Use specific column names instead of `SELECT *`.
**Don'ts:**
- Don’t fetch unnecessary data to avoid performance issues.

#### 3. **DML (Data Manipulation Language)**
Commands used to manipulate data in tables.
- **INSERT**: Adds new records.
- **UPDATE**: Modifies existing records.
- **DELETE**: Removes records.

**Do's:**
- Use `WHERE` in `UPDATE` and `DELETE` to avoid unintended changes.
- Validate input data.
**Don'ts:**
- Don’t update or delete records without conditions.

---

### Data Operations

#### Insert Multiple Columns Data
**CODE:**
```sql
INSERT INTO employees (name, age, department)
VALUES
('Alice', 30, 'HR'),
('Bob', 25, 'IT'),
('Charlie', 40, 'Finance');
```

#### Insert Partial Fields
**CODE:**
```sql
INSERT INTO employees (name, department)
VALUES ('Diana', 'Marketing');
```

#### Update Query
**CODE:**
```sql
UPDATE employees
SET department = 'Sales'
WHERE id = 2;
```

---

### MySQL Select Queries

#### Select Query (All Fields)
**CODE:**
```sql
SELECT * FROM employees;
```

#### Select Specific Fields
**CODE:**
```sql
SELECT name, department FROM employees;
```

---

### Table Alterations

#### Add Multiple Columns
**CODE:**
```sql
ALTER TABLE employees
ADD COLUMN hire_date DATE,
ADD COLUMN salary DECIMAL(10, 2);
```

#### Modify Column
**CODE:**
```sql
ALTER TABLE employees
MODIFY COLUMN age TINYINT NOT NULL;
```

#### Drop Column
**CODE:**
```sql
ALTER TABLE employees
DROP COLUMN hire_date;
```

#### Rename Column
**CODE:**
```sql
ALTER TABLE employees
CHANGE COLUMN salary annual_salary DECIMAL(10, 2);
```

#### Rename Table
**CODE:**
```sql
RENAME TABLE employees TO staff;
```

---

### Table and Data Management

#### Truncate Table
**CODE:**
```sql
TRUNCATE TABLE staff;
```

---

### MySQL Views

#### Create View
**CODE:**
```sql
CREATE VIEW department_summary AS
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

#### Update View
**CODE:**
```sql
CREATE OR REPLACE VIEW department_summary AS
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

#### Drop View
**CODE:**
```sql
DROP VIEW department_summary;
```

---

### Additional Queries

#### Insert Query
**CODE:**
```sql
INSERT INTO employees (name, age, department)
VALUES ('Eve', 35, 'Legal');
```

#### MySQL Delete Statement
**CODE:**
```sql
DELETE FROM employees
WHERE id = 3;
```

