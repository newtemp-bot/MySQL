## **1. Inner Queries (Subqueries)**
An **Inner Query** (also called a **Subquery**) is a query nested inside another query. It is executed first, and its result is used by the outer query.

### **Types of Subqueries**
- **Scalar Subquery**: Returns a single value.
- **Single-Row Subquery**: Returns one row with multiple columns.
- **Multi-Row Subquery**: Returns multiple rows.
- **Correlated Subquery**: Uses values from the outer query.

---

### **1.1. Table and Sample Data**
Let's create tables for the examples:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10,2),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

**Insert Sample Data:**
```sql
INSERT INTO departments VALUES (1, 'IT'), (2, 'HR'), (3, 'Finance');

INSERT INTO employees VALUES 
(1, 'Alice', 60000, 1),
(2, 'Bob', 50000, 1),
(3, 'Charlie', 70000, 2),
(4, 'David', 80000, 3),
(5, 'Emma', 45000, 2);
```

---

### **1.2. Scalar Subquery**
A subquery that returns a **single value**.

**Example:** Find employees who earn more than the **average salary**.
```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

### **1.3. Single-Row Subquery**
Returns **one row** but can have multiple columns.

**Example:** Get the highest-paid employee’s name and salary.
```sql
SELECT name, salary
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

---

### **1.4. Multi-Row Subquery**
Returns **multiple rows**.

**Example:** Get names of employees working in the **HR department**.
```sql
SELECT name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE department_name = 'HR');
```

---

### **1.5. Correlated Subquery**
A correlated subquery runs **once per row** of the outer query.

**Example:** Find employees who earn more than the **average salary of their department**.
```sql
SELECT name, salary
FROM employees e1
WHERE salary > (SELECT AVG(salary) FROM employees e2 WHERE e1.department_id = e2.department_id);
```

---

## **2. Stored Procedures**
A **Stored Procedure** is a set of SQL statements that can be executed **multiple times** by calling it.

### **2.1. Creating a Simple Stored Procedure**
This procedure returns employees **earning more than** a given salary.

```sql
DELIMITER $$

CREATE PROCEDURE GetHighSalaryEmployees(IN min_salary DECIMAL(10,2))
BEGIN
    SELECT * FROM employees WHERE salary > min_salary;
END $$

DELIMITER ;
```

#### **Calling the Procedure:**
```sql
CALL GetHighSalaryEmployees(50000);
```

---

### **2.2. Stored Procedure with Output Parameter**
This procedure returns the **count of employees** in a department.

```sql
DELIMITER $$

CREATE PROCEDURE CountEmployees(IN dept_id INT, OUT emp_count INT)
BEGIN
    SELECT COUNT(*) INTO emp_count FROM employees WHERE department_id = dept_id;
END $$

DELIMITER ;
```

#### **Calling the Procedure:**
```sql
CALL CountEmployees(1, @total_employees);
SELECT @total_employees; -- Output: Total employees in department 1
```

---

### **2.3. Stored Procedure with Multiple Parameters**
Find the **highest salary** in a given department.

```sql
DELIMITER $$

CREATE PROCEDURE GetMaxSalary(IN dept_id INT, OUT max_salary DECIMAL(10,2))
BEGIN
    SELECT MAX(salary) INTO max_salary FROM employees WHERE department_id = dept_id;
END $$

DELIMITER ;
```

#### **Calling the Procedure:**
```sql
CALL GetMaxSalary(2, @max_sal);
SELECT @max_sal; -- Output: Max salary in department 2
```

---

### **2.4. Stored Procedure with Loop**
Print numbers **from 1 to N**.

```sql
DELIMITER $$

CREATE PROCEDURE PrintNumbers(IN n INT)
BEGIN
    DECLARE counter INT DEFAULT 1;
    
    WHILE counter <= n DO
        SELECT counter;
        SET counter = counter + 1;
    END WHILE;
END $$

DELIMITER ;
```

#### **Calling the Procedure:**
```sql
CALL PrintNumbers(5);
```

---

### **2.5. Stored Procedure with IF-ELSE Condition**
Check if a **department exists** before inserting an employee.

```sql
DELIMITER $$

CREATE PROCEDURE InsertEmployee(
    IN emp_name VARCHAR(50), 
    IN emp_salary DECIMAL(10,2), 
    IN dept_id INT
)
BEGIN
    DECLARE dept_exists INT;
    
    SELECT COUNT(*) INTO dept_exists FROM departments WHERE department_id = dept_id;

    IF dept_exists > 0 THEN
        INSERT INTO employees (name, salary, department_id) VALUES (emp_name, emp_salary, dept_id);
    ELSE
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Department does not exist';
    END IF;
END $$

DELIMITER ;
```

#### **Calling the Procedure:**
```sql
CALL InsertEmployee('John', 55000, 1);
```

---

## **3. Best Practices for Subqueries & Stored Procedures**
### **Best Practices for Subqueries**
✅ Use **indexed columns** in subqueries to improve performance.  
✅ Use **`EXISTS` instead of `IN`** for large data sets.  
✅ Use **joins** instead of subqueries where possible for better performance.  

### **Best Practices for Stored Procedures**
✅ Use **meaningful names** for stored procedures.  
✅ **Handle errors** using `SIGNAL SQLSTATE`.  
✅ Use **transactions** (`START TRANSACTION`, `COMMIT`, `ROLLBACK`) for important data updates.  

### **Transaction Query Language (TQL) in MySQL**  

**TQL (Transaction Query Language)** deals with **transactions** in MySQL. It includes commands to manage transactions like `COMMIT`, `ROLLBACK`, and `SAVEPOINT`, ensuring **data consistency and integrity**.

---

## **1. What is a Transaction?**  
A **transaction** is a sequence of **one or more SQL operations** performed as a **single unit of work**. Transactions **follow ACID properties**:
- **A**tomicity → All operations in a transaction are executed or none at all.
- **C**onsistency → Data integrity is maintained.
- **I**solation → Transactions do not interfere with each other.
- **D**urability → Changes are permanent after commit.

---

## **2. Enabling Transactions in MySQL**  
By default, MySQL **autocommits** changes. To use transactions, disable `autocommit`:

```sql
SET AUTOCOMMIT = 0;  -- Disable auto commit
```

To **re-enable** auto-commit:
```sql
SET AUTOCOMMIT = 1;
```

---

## **3. MySQL Transaction Commands**

### **3.1. START TRANSACTION**
Begins a new transaction.

**Syntax:**
```sql
START TRANSACTION;
```

---

### **3.2. COMMIT**
Saves all changes made during the transaction.

**Syntax:**
```sql
COMMIT;
```

**Example:**
```sql
START TRANSACTION;

UPDATE employees SET salary = salary + 5000 WHERE department_id = 1;
INSERT INTO employees (name, salary, department_id) VALUES ('John', 60000, 1);

COMMIT;
```

---

### **3.3. ROLLBACK**
Undoes all changes since the last `START TRANSACTION` or `SAVEPOINT`.

**Syntax:**
```sql
ROLLBACK;
```

**Example:**
```sql
START TRANSACTION;

UPDATE employees SET salary = salary + 5000 WHERE department_id = 2;
DELETE FROM employees WHERE employee_id = 5;

ROLLBACK; -- Undo the update and delete
```

---

### **3.4. SAVEPOINT**
Creates a point in a transaction to which changes can be **rolled back partially**.

**Syntax:**
```sql
SAVEPOINT savepoint_name;
```

**Example:**
```sql
START TRANSACTION;

UPDATE employees SET salary = salary + 5000 WHERE department_id = 1;
SAVEPOINT before_delete;

DELETE FROM employees WHERE employee_id = 3;

ROLLBACK TO before_delete; -- Undo only the DELETE operation

COMMIT; -- Save the salary update
```

---

### **3.5. RELEASE SAVEPOINT**
Deletes a specific savepoint so it can no longer be rolled back.

**Syntax:**
```sql
RELEASE SAVEPOINT savepoint_name;
```

**Example:**
```sql
START TRANSACTION;

UPDATE employees SET salary = salary + 5000 WHERE department_id = 1;
SAVEPOINT salary_update;

DELETE FROM employees WHERE employee_id = 3;

RELEASE SAVEPOINT salary_update; -- Cannot rollback to this point anymore

COMMIT;
```

---

## **4. Practical Use Case Example**
### **Managing Employee Salaries**
1. **Increase salary by 10% for all employees in IT.**
2. **If more than 2 employees get an update, commit. Otherwise, rollback.**

```sql
START TRANSACTION;

UPDATE employees 
SET salary = salary * 1.10 
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'IT');

SET @row_count = ROW_COUNT(); -- Get number of affected rows

IF @row_count > 2 THEN
    COMMIT;
ELSE
    ROLLBACK;
END IF;
```

---

## **5. Best Practices for Transactions in MySQL**
✅ **Use transactions for critical operations** (e.g., financial updates).  
✅ **Always commit or rollback** at the end of a transaction.  
✅ **Use SAVEPOINTS** for better rollback control in multi-step transactions.  
✅ **Use proper indexing** for performance optimization.  
✅ **Avoid long transactions**, as they can lock tables and reduce database performance.  