### **MySQL: Comprehensive Guide to Foreign Keys, Joins, and Functions**

---

## **1. Foreign Keys in MySQL**

### **What is a Foreign Key?**
A `FOREIGN KEY` is a column or combination of columns used to establish a link between the data in two tables. It enforces referential integrity by ensuring that the value in the foreign key column matches a primary key value in the referenced table.

---

#### **A. Creating Foreign Keys**

##### **Step 1: Create Parent Table**
The parent table must have a `PRIMARY KEY` or `UNIQUE` column to be referenced.

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);
```

##### **Step 2: Create Child Table with a Foreign Key**
Define a foreign key in the child table to reference the parent table's primary key.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    department_id INT,
    CONSTRAINT fk_department FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

---

##### **B. Adding a Foreign Key to an Existing Table**
**Syntax:**
```sql
ALTER TABLE child_table
ADD CONSTRAINT constraint_name FOREIGN KEY (column_name) REFERENCES parent_table(parent_column);
```

**Example:**
```sql
ALTER TABLE orders
ADD CONSTRAINT fk_customer FOREIGN KEY (customer_id) REFERENCES customers(customer_id);
```

---

##### **C. Dropping a Foreign Key**
**Syntax:**
```sql
ALTER TABLE child_table
DROP FOREIGN KEY constraint_name;
```

**Example:**
```sql
ALTER TABLE orders
DROP FOREIGN KEY fk_customer;
```

---

#### **Best Practices for Foreign Keys**
1. Use **indexed columns** for referenced keys to improve performance.
2. Avoid cyclic dependencies between tables.
3. Use `ON DELETE` and `ON UPDATE` actions:
   - `CASCADE`: Propagates changes to the child table.
   - `SET NULL`: Sets child values to `NULL`.
   - `NO ACTION` or `RESTRICT`: Prevents parent deletion/update if related records exist.

**Example:**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE CASCADE ON UPDATE CASCADE
);
```

## **2. MySQL Joins**

Joins combine rows from two or more tables based on a related column.

---

### **1. Inner Join**
- Returns only the rows that have matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

**Example:**
```sql
SELECT employees.employee_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```

---

### **2. Left Outer Join**
- Returns all rows from the left table, with matching rows from the right table. Fills unmatched rows with `NULL`.

**Syntax:**
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

**Example:**
```sql
SELECT employees.employee_name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id;
```

---

### **3. Right Outer Join**
- Returns all rows from the right table, with matching rows from the left table. Fills unmatched rows with `NULL`.

**Syntax:**
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

**Example:**
```sql
SELECT employees.employee_name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.department_id;
```

---

### **4. Full Outer Join (Not Directly Supported in MySQL)**
MySQL doesn’t support `FULL OUTER JOIN` directly. Use `UNION` of `LEFT JOIN` and `RIGHT JOIN` to achieve the same result.

**Example:**
```sql
SELECT employees.employee_name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id
UNION
SELECT employees.employee_name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.department_id;
```

---

## **3. Functions in MySQL**

### **What are Functions?**
Functions in MySQL are reusable blocks of SQL code that perform a specific task. There are two types:
1. **Built-in Functions**: Predefined by MySQL.
2. **User-Defined Functions (UDFs)**: Custom functions created by users.

---

### **Types of Built-In Functions**

1. **Aggregate Functions**:
   - Perform calculations on a set of values and return a single value.
   - Examples: `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

2. **String Functions**:
   - Manipulate strings.
   - Examples: `CONCAT()`, `LENGTH()`, `SUBSTRING()`, `UPPER()`.

3. **Date and Time Functions**:
   - Handle date and time operations.
   - Examples: `NOW()`, `CURDATE()`, `DATE_ADD()`, `DATEDIFF()`.

4. **Mathematical Functions**:
   - Perform numeric calculations.
   - Examples: `ROUND()`, `CEIL()`, `FLOOR()`, `MOD()`.

---

### **1. Aggregate Functions**

Aggregate functions are used to perform calculations on a set of values and return a single value.

#### **SUM()**
Returns the sum of a numeric column.

**Example:**
```sql
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;
```

#### **AVG()**
Returns the average value of a numeric column.

**Example:**
```sql
SELECT department_id, AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

#### **COUNT()**
Returns the number of rows that match a specified condition.

**Example:**
```sql
SELECT department_id, COUNT(*) AS total_employees
FROM employees
GROUP BY department_id;
```

#### **MIN()**
Returns the minimum value of a column.

**Example:**
```sql
SELECT department_id, MIN(salary) AS lowest_salary
FROM employees
GROUP BY department_id;
```

#### **MAX()**
Returns the maximum value of a column.

**Example:**
```sql
SELECT department_id, MAX(salary) AS highest_salary
FROM employees
GROUP BY department_id;
```

---

### **2. String Functions**

String functions are used to manipulate string data types.

#### **CONCAT()**
Concatenates two or more strings.

**Example:**
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

#### **LENGTH()**
Returns the length of a string (in characters).

**Example:**
```sql
SELECT first_name, LENGTH(first_name) AS name_length
FROM employees;
```

#### **SUBSTRING()**
Extracts a substring from a string.

**Example:**
```sql
SELECT SUBSTRING(first_name, 1, 3) AS name_part
FROM employees;
```

#### **UPPER()**
Converts a string to uppercase.

**Example:**
```sql
SELECT UPPER(first_name) AS uppercase_name
FROM employees;
```

#### **LOWER()**
Converts a string to lowercase.

**Example:**
```sql
SELECT LOWER(last_name) AS lowercase_name
FROM employees;
```

#### **TRIM()**
Removes leading and trailing spaces from a string.

**Example:**
```sql
SELECT TRIM(first_name) AS trimmed_name
FROM employees;
```

#### **REPLACE()**
Replaces occurrences of a substring within a string.

**Example:**
```sql
SELECT REPLACE(phone_number, '-', '') AS cleaned_phone
FROM employees;
```

---

### **3. Date and Time Functions**

Date and time functions handle date and time operations.

#### **NOW()**
Returns the current date and time.

**Example:**
```sql
SELECT NOW() AS current_datetime;
```

#### **CURDATE()**
Returns the current date.

**Example:**
```sql
SELECT CURDATE() AS current_date;
```

#### **DATE_ADD()**
Adds a specified time interval to a date.

**Example:**
```sql
SELECT DATE_ADD(CURDATE(), INTERVAL 10 DAY) AS future_date;
```

#### **DATEDIFF()**
Returns the number of days between two dates.

**Example:**
```sql
SELECT DATEDIFF('2025-12-31', '2025-01-01') AS days_difference;
```

#### **YEAR()**
Extracts the year from a date.

**Example:**
```sql
SELECT YEAR(order_date) AS order_year
FROM orders;
```

#### **MONTH()**
Extracts the month from a date.

**Example:**
```sql
SELECT MONTH(order_date) AS order_month
FROM orders;
```

#### **DAY()**
Extracts the day from a date.

**Example:**
```sql
SELECT DAY(order_date) AS order_day
FROM orders;
```

---

### **4. Mathematical Functions**

Mathematical functions are used to perform numeric calculations.

#### **ROUND()**
Rounds a number to a specified number of decimal places.

**Example:**
```sql
SELECT ROUND(salary, 2) AS rounded_salary
FROM employees;
```

#### **CEIL()**
Returns the smallest integer greater than or equal to a given number.

**Example:**
```sql
SELECT CEIL(salary) AS rounded_up_salary
FROM employees;
```

#### **FLOOR()**
Returns the largest integer less than or equal to a given number.

**Example:**
```sql
SELECT FLOOR(salary) AS rounded_down_salary
FROM employees;
```

#### **MOD()**
Returns the remainder of a division.

**Example:**
```sql
SELECT MOD(salary, 1000) AS salary_remainder
FROM employees;
```

#### **ABS()**
Returns the absolute value of a number.

**Example:**
```sql
SELECT ABS(-100) AS absolute_value;
```

#### **POW()**
Returns the value of a number raised to the power of another.

**Example:**
```sql
SELECT POW(2, 3) AS power_value; -- 2^3 = 8
```

#### **SQRT()**
Returns the square root of a number.

**Example:**
```sql
SELECT SQRT(16) AS square_root; -- 4
```

---

### **Best Practices**
1. **Aggregation with GROUP BY**: Always use `GROUP BY` when using aggregate functions to group rows by a specific column.
2. **Optimize String Functions**: Use string functions wisely, especially on large datasets, as they can be resource-intensive.
3. **Date Handling**: When working with date and time, always ensure you're using the correct format (`YYYY-MM-DD` for date and `YYYY-MM-DD HH:MM:SS` for datetime).
4. **Mathematical Calculations**: Be cautious when rounding numbers or using `FLOOR` and `CEIL` to avoid unexpected results.

---

### **4. Creating User-Defined Functions**

#### **Steps to Create a Function**

1. **Define the Function:**
   Use the `CREATE FUNCTION` statement.

2. **Specify Parameters:**
   Define input parameters (if any) and the return type.

3. **Write the Function Body:**
   Include the SQL logic inside `BEGIN` and `END`.

4. **Set Return Values:**
   Use the `RETURN` statement to specify the output.

---

#### **Syntax**
```sql
DELIMITER $$

CREATE FUNCTION function_name (parameter_name datatype)
RETURNS return_datatype
DETERMINISTIC
BEGIN
    -- Function body
    RETURN value;
END $$

DELIMITER ;
```

---

### **Examples**

#### **1. Simple Function**
A function to calculate the square of a number:
```sql
DELIMITER $$

CREATE FUNCTION square(num INT)
RETURNS INT
DETERMINISTIC
BEGIN
    RETURN num * num;
END $$

DELIMITER ;
```

**Usage:**
```sql
SELECT square(5); -- Output: 25
```

---

#### **2. Function with String Operations**
A function to concatenate first and last names:
```sql
DELIMITER $$

CREATE FUNCTION full_name(first_name VARCHAR(50), last_name VARCHAR(50))
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    RETURN CONCAT(first_name, ' ', last_name);
END $$

DELIMITER ;
```

**Usage:**
```sql
SELECT full_name('John', 'Doe'); -- Output: John Doe
```

---

### **5. Use of Functions**

#### **Use Case 1: Calculations**
Functions simplify repetitive calculations in queries.

**Example:**
```sql
SELECT employee_name, square(salary) AS salary_squared
FROM employees;
```

#### **Use Case 2: Business Logic**
Use functions to encapsulate complex business rules.

#### **Use Case 3: Data Transformation**
Format or modify data using functions.

**Example:**
```sql
SELECT full_name(first_name, last_name) AS employee_name
FROM employees;
```

---

### **6. First and Last Functions**

#### **First Value**
MySQL doesn’t have a direct `FIRST()` function, but you can use `ORDER BY` and `LIMIT` to fetch the first value:
```sql
SELECT employee_name
FROM employees
ORDER BY hire_date ASC
LIMIT 1;
```

#### **Last Value**
MySQL doesn’t have a direct `LAST()` function, but you can use `ORDER BY` and `LIMIT`:
```sql
SELECT employee_name
FROM employees
ORDER BY hire_date DESC
LIMIT 1;
```

---

### **Best Practices**
1. Use functions sparingly in queries with large datasets to avoid performance bottlenecks.
2. Always test user-defined functions thoroughly before deploying them.
3. Index foreign key columns to optimize joins.

---