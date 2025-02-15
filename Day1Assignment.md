### **Database Name:** `SchoolDB`  

#### **Table: Student**
| Column Name | Data Type | Constraints |
|-------------|----------|-------------|
| `StudentID` | `INT` | `PRIMARY KEY` |
| `Name` | `VARCHAR(50)` | `NOT NULL` |
| `Age` | `INT` | `DEFAULT 18` |

#### **Table: Course**
| Column Name | Data Type | Constraints |
|-------------|----------|-------------|
| `CourseID` | `INT` | `PRIMARY KEY` |
| `CourseName` | `VARCHAR(100)` | `NOT NULL` |
| `Duration` | `INT` | `DEFAULT 6` |

#### **Table: Enrollment**
| Column Name | Data Type | Constraints |
|-------------|----------|-------------|
| `EnrollmentID` | `INT` | `PRIMARY KEY` |
| `StudentID` | `INT` | `NOT NULL` |
| `CourseID` | `INT` | `NOT NULL` |

---

## **20 Practical Questions**  

### **1-3: CREATE DATABASE**
1. Write a MySQL query to create a database named `SchoolDB`.  
2. Create a database named `LibraryDB` in MySQL.  
3. Write a query to create a database called `CompanyDB` and use it.  

---

### **4-7: CREATE TABLE**
4. Write a MySQL query to create the `Student` table as per the blueprint.  
5. Write an SQL query to create the `Course` table as per the blueprint.  
6. Write an SQL query to create the `Enrollment` table as per the blueprint.  
7. Write a MySQL query to create an `Employee` table with:  
   - `EmpID` (Primary Key, Integer)  
   - `EmpName` (Not Null, String of 50 characters)  
   - `Salary` (Integer, Default 25000)  

---

### **8-13: INSERT INTO**
8. Insert a student into the `Student` table with:  
   - `StudentID = 1`, `Name = 'John Doe'`, `Age = 20`  

9. Add another student into the `Student` table:  
   - `StudentID = 2`, `Name = 'Alice Smith'`  
   *(Do not provide Age; check if the default value works)*  

10. Insert a course into the `Course` table:  
   - `CourseID = 101`, `CourseName = 'Mathematics'`, `Duration = 12`  

11. Add a new course into the `Course` table:  
   - `CourseID = 102`, `CourseName = 'Physics'`  
   *(Do not provide Duration; check if the default value works)*  

12. Enroll a student into a course using the `Enrollment` table:  
   - `EnrollmentID = 1`, `StudentID = 1`, `CourseID = 101`  

13. Insert an employee into the `Employee` table:  
   - `EmpID = 1`, `EmpName = 'Robert Brown'`, `Salary = 30000`  

---

### **14-16: TRUNCATE TABLE**
14. Write an SQL query to remove all records from the `Student` table without deleting the table structure.  
15. Remove all data from the `Course` table but keep its structure.  
16. Write a MySQL query to clear all records from the `Enrollment` table while keeping its structure.  

---

### **17-20: DROP TABLE & DROP DATABASE**
17. Write a MySQL query to delete the `Student` table.  
18. Drop the `Course` table from MySQL.  
19. Write an SQL query to remove the `Enrollment` table if it exists.  
20. Write a MySQL query to delete the `SchoolDB` database.  
