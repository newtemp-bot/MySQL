### **SQL Clauses and Conditions: Rules, Syntax, and Best Practices**

---

### **HAVING Clause**
The `HAVING` clause is used to filter aggregated results, often in combination with the `GROUP BY` clause.

**Syntax:**
```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

**Example:**
```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

### **LIKE Operator**
The `LIKE` operator is used to search for a specified pattern in a column. 

#### **Wildcards for `LIKE`:**
- `%`: Matches zero or more characters.
- `_`: Matches exactly one character.

#### **In MS SQL Server you Can Use**
- `[ ]`: Matches any single character within the specified set (e.g., `[abc]` matches `a`, `b`, or `c`).
- `[! ]` or `[^ ]`: Matches any single character not within the specified set (e.g., `[!abc]` matches any character except `a`, `b`, or `c`).

**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE column1 LIKE pattern;
```

#### **Examples:**
- **Using `%`**:
  ```sql
  SELECT name
  FROM students
  WHERE name LIKE 'A%'; -- Names starting with 'A'
  ```
- **Using `_`**:
  ```sql
  SELECT name
  FROM students
  WHERE name LIKE 'J_n'; -- Matches 'Jon', 'Jan', etc.
  ```
- **Using `[ ]`**:
  ```sql
  SELECT name
  FROM students
  WHERE name LIKE '[AB]%'; -- Names starting with 'A' or 'B'
  ```
- **Using `[! ]`**:
  ```sql
  SELECT name
  FROM students
  WHERE name LIKE '[!A]%'; -- Names not starting with 'A'
  ```

---

### **NOT Operator**
The `NOT` operator negates a condition.

**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE NOT condition;
```

**Example:**
```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

---

### **IN Condition**
The `IN` condition checks if a value matches any value in a specified list.

**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE column1 IN (value1, value2, ...);
```

**Example:**
```sql
SELECT name
FROM students
WHERE grade IN ('A', 'B');
```

---

### **NOT IN Condition**
The `NOT IN` condition checks if a value does not match any value in a specified list.

**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE column1 NOT IN (value1, value2, ...);
```

**Example:**
```sql
SELECT name
FROM students
WHERE grade NOT IN ('D', 'F');
```

---

### **IS NULL Condition**
The `IS NULL` condition checks for `NULL` values.

**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE column1 IS NULL;
```

**Example:**
```sql
SELECT name
FROM employees
WHERE manager_id IS NULL;
```

---

### **IS NOT NULL Condition**
The `IS NOT NULL` condition checks for non-`NULL` values.

**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE column1 IS NOT NULL;
```

**Example:**
```sql
SELECT name
FROM employees
WHERE manager_id IS NOT NULL;
```

---

### **BETWEEN Operator**
The `BETWEEN` operator filters values within a specified range.

#### **With Numeric Values**
**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE column1 BETWEEN value1 AND value2;
```

**Example:**
```sql
SELECT name
FROM students
WHERE age BETWEEN 18 AND 25;
```

#### **With Dates**
**Syntax:**
```sql
SELECT column1
FROM table_name
WHERE date_column BETWEEN 'start_date' AND 'end_date';
```

**Example:**
```sql
SELECT order_id
FROM orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31';
```

---

### **Advanced Wildcards for `LIKE`:**
1. **Escaping Special Characters:**
   If your pattern contains `%`, `_`, or `[ ]` as literals, escape them using `ESCAPE`:
   ```sql
   SELECT name
   FROM employees
   WHERE name LIKE '50\%' ESCAPE '\'; -- Matches '50%'
   ```
#### **Only Use in MS SQL Server**
2. **Combining Wildcards:**
   ```sql
   SELECT name
   FROM employees
   WHERE name LIKE '%Smith_' AND name LIKE '[!A-Z]%';
   ```

---

### Best Practices
1. **Index Optimization:**
   - Avoid using `%` at the start of the pattern as it disables index usage.
   - Example to avoid: `LIKE '%pattern%'`.

2. **Combine Operators:**
   - Use `AND`, `OR`, and parentheses for clarity in complex queries.
   - Example:
     ```sql
     SELECT *
     FROM employees
     WHERE (department = 'IT' AND salary > 50000) OR manager_id IS NULL;
     ```

3. **Testing with Boundaries:**
   - Test `BETWEEN` with inclusive start and end values.

4. **NULL Handling:**
   - Use `IS NULL` and `IS NOT NULL` explicitly, as equality (`=`) does not work with `NULL`.

5. **Avoid Redundant Conditions:**
   - Instead of:
     ```sql
     SELECT *
     FROM employees
     WHERE salary >= 50000 AND salary <= 100000;
     ```
     Use:
     ```sql
     SELECT *
     FROM employees
     WHERE salary BETWEEN 50000 AND 100000;
     ```

Here’s an exhaustive list of examples covering **all possible scenarios** for using `CHECK` constraints while creating and modifying tables in SQL:

---

### **General Syntax for `CHECK` Constraints**

1. **Column-Level**:
   ```sql
   column_name datatype CHECK (condition)
   ```

2. **Table-Level**:
   ```sql
   CONSTRAINT constraint_name CHECK (condition)
   ```

---

### **Examples of `CHECK` Constraints**

#### **1. Numeric Range Validation**
- Ensure a column's value falls within a specific range.
```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    age INT CHECK (age BETWEEN 18 AND 25)
);
```

---

#### **2. Specific Value Validation**
- Restrict a column to specific values using `IN`.
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    job_role VARCHAR(50) CHECK (job_role IN ('Manager', 'Developer', 'Tester'))
);
```

---

#### **3. Greater Than / Less Than Conditions**
- Ensure numerical values meet conditions.
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    quantity INT CHECK (quantity > 0),
    price DECIMAL(10, 2) CHECK (price <= 10000)
);
```

---

#### **4. Date Validation**
- Validate date ranges.
```sql
CREATE TABLE events (
    event_id INT PRIMARY KEY,
    event_date DATE CHECK (event_date >= '2023-01-01')
);
```

---

#### **5. Multiple Conditions on a Single Column**
- Combine conditions with logical operators.
```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10, 2) CHECK (balance >= 0 AND balance <= 100000)
);
```

---

#### **6. Multiple Columns Validation**
- Use table-level constraints for interdependent columns.
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    salary DECIMAL(10, 2),
    bonus DECIMAL(10, 2),
    CONSTRAINT chk_salary_bonus CHECK (salary >= bonus)
);
```

---

#### **7. Restrict Based on String Patterns**
- Use `LIKE` in constraints (specific to some DBMS).
```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) CHECK (email LIKE '%@%.%')
);
```

---

#### **8. Value Cannot Be Zero**
```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    weight DECIMAL(10, 2) CHECK (weight > 0)
);
```

---

#### **9. Boolean Conditions**
- Enforce binary choices (e.g., Yes/No or 0/1).
```sql
CREATE TABLE registrations (
    reg_id INT PRIMARY KEY,
    is_active TINYINT CHECK (is_active IN (0, 1))
);
```

---

#### **10. Gender Restriction**
- Allow only specific gender values.
```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    gender CHAR(1) CHECK (gender IN ('M', 'F', 'O'))
);
```

---

#### **11. Age Validation**
```sql
CREATE TABLE participants (
    participant_id INT PRIMARY KEY,
    age INT CHECK (age >= 18 AND age <= 60)
);
```

---

#### **12. Dependent Column Constraints**
- Validate based on another column's value.
```sql
CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    discount DECIMAL(5, 2),
    total_amount DECIMAL(10, 2),
    CONSTRAINT chk_discount CHECK (discount <= total_amount * 0.5)
);
```

---

#### **13. Prevent Negative Values**
```sql
CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY,
    amount DECIMAL(10, 2) CHECK (amount >= 0)
);
```

---

#### **14. Name Restrictions**
- Allow only names starting with a specific letter.
```sql
CREATE TABLE authors (
    author_id INT PRIMARY KEY,
    name VARCHAR(50) CHECK (name LIKE 'A%')
);
```

---

#### **15. Compound Conditions**
- Complex business rules combining multiple conditions.
```sql
CREATE TABLE invoices (
    invoice_id INT PRIMARY KEY,
    invoice_date DATE,
    payment_date DATE,
    CONSTRAINT chk_dates CHECK (payment_date >= invoice_date)
);
```

---

### **Modifying Tables with `CHECK` Constraints**

#### **1. Adding a `CHECK` Constraint**
- Add constraints after the table is created.
```sql
ALTER TABLE students
ADD CONSTRAINT chk_age CHECK (age >= 18);
```

#### **2. Dropping a `CHECK` Constraint**
```sql
ALTER TABLE students
DROP CONSTRAINT chk_age;
```

#### **3. Rename a `CHECK` Constraint (Workaround via Drop and Add)**
```sql
ALTER TABLE students
DROP CONSTRAINT chk_age;

ALTER TABLE students
ADD CONSTRAINT chk_age_new CHECK (age >= 18);
```

---

### **Combining `CHECK` with Other Constraints**

#### **1. Using `CHECK` with `NOT NULL`**
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    salary DECIMAL(10, 2) NOT NULL CHECK (salary > 0)
);
```

#### **2. Using `CHECK` with `FOREIGN KEY`**
```sql
CREATE TABLE projects (
    project_id INT PRIMARY KEY,
    department_id INT,
    CONSTRAINT fk_department FOREIGN KEY (department_id) REFERENCES departments(department_id),
    CONSTRAINT chk_department_id CHECK (department_id > 0)
);
```

---

### **Best Practices for `CHECK` Constraints**
1. **Descriptive Names**:
   Always use meaningful names for constraints.
   ```sql
   CONSTRAINT chk_positive_salary CHECK (salary > 0)
   ```

2. **Test Business Rules**:
   Use test cases to ensure constraints cover all edge cases (e.g., boundaries, nulls).

3. **Use Indexes**:
   Pair constraints with indexed columns to optimize performance during validation.

4. **Avoid Redundant Constraints**:
   Don’t duplicate validations already handled in the application logic.

5. **Keep Conditions Simple**:
   Complex constraints can be hard to maintain and may reduce performance.