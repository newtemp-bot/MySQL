### SQL Clauses and Conditions: Rules, Syntax, and Best Practices

---

### **WHERE Clause**
The `WHERE` clause is used to filter records based on specific conditions.

**Syntax:**
```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

**Do's:**
- Use appropriate comparison operators (`=`, `<`, `>`, `LIKE`, etc.)
- Combine with `AND` or `OR` for multiple conditions.

**Don'ts:**
- Avoid using the `WHERE` clause without understanding the data types of columns.
- Don’t forget to test with boundary values.

**Example:**
```sql
SELECT *
FROM students
WHERE age > 18;
```

---

### **AND Condition**
The `AND` condition is used to combine multiple conditions. All conditions must be true.

**Syntax:**
```sql
SELECT column1, column2
FROM table_name
WHERE condition1 AND condition2;
```

**Example:**
```sql
SELECT *
FROM employees
WHERE department = 'IT' AND salary > 50000;
```

---

### **OR Condition**
The `OR` condition is used to combine multiple conditions. At least one condition must be true.

**Syntax:**
```sql
SELECT column1, column2
FROM table_name
WHERE condition1 OR condition2;
```

**Example:**
```sql
SELECT *
FROM products
WHERE category = 'Electronics' OR price < 100;
```

---

### **AND & OR Conditions**
Combine `AND` and `OR` conditions for more complex queries. Use parentheses for clarity.

**Syntax:**
```sql
SELECT column1, column2
FROM table_name
WHERE (condition1 AND condition2) OR condition3;
```

**Example:**
```sql
SELECT *
FROM orders
WHERE (status = 'shipped' AND payment_status = 'paid') OR total_amount > 1000;
```

**Do's:**
- Use parentheses for better readability and logical grouping.
- Test each condition individually before combining.

**Don'ts:**
- Avoid ambiguous combinations without parentheses.

---

### **DISTINCT Clause**
The `DISTINCT` clause is used to remove duplicate rows from the result set.

**Syntax:**
```sql
SELECT DISTINCT column1
FROM table_name;
```

#### **With Single Expression**
**Example:**
```sql
SELECT DISTINCT city
FROM customers;
```

#### **With Multiple Expressions**
**Example:**
```sql
SELECT DISTINCT city, state
FROM customers;
```

**Do's:**
- Use `DISTINCT` when duplicates need to be removed.

**Don'ts:**
- Avoid using `DISTINCT` unnecessarily as it can impact performance.

---

### **FROM Clause**
The `FROM` clause specifies the table to retrieve data from.

**Syntax:**
```sql
SELECT column1, column2
FROM table_name;
```

**Example:**
```sql
SELECT name, age
FROM students;
```

**Do's:**
- Specify the correct table name.

**Don'ts:**
- Don’t use ambiguous table names in complex queries without aliases.

---

### **ORDER BY Clause**
The `ORDER BY` clause is used to sort the result set in ascending (`ASC`) or descending (`DESC`) order.

**Syntax:**
```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 ASC/DESC;
```

**Example:**
- **Ascending Order:**
  ```sql
  SELECT name, age
  FROM students
  ORDER BY age ASC;
  ```
- **Descending Order:**
  ```sql
  SELECT name, age
  FROM students
  ORDER BY age DESC;
  ```

**Do's:**
- Use explicit `ASC` or `DESC` to avoid confusion.

**Don'ts:**
- Don’t sort unnecessarily for large datasets without proper indexing.

---

### **GROUP BY Clause**
The `GROUP BY` clause groups rows sharing a property so aggregate functions can be applied.

**Syntax:**
```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```

**Example:**
```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**Do's:**
- Use aggregate functions like `SUM`, `AVG`, `COUNT` with `GROUP BY`.

**Don'ts:**
- Avoid using columns in the `SELECT` list that are not in the `GROUP BY` clause or an aggregate function.

---

