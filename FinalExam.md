## **📌 MySQL Practical Exam (100 Marks)**
**Duration:** 2.5 Hours  
**Instructions:**  
- Create all tables with correct **Primary and Foreign Key constraints**.  
- Insert the given **sample data** into the tables.  
- Answer **all 50 practical questions** using MySQL queries.  
- Each question carries **2 marks**.  

---

# **💾 Database Scenario: University Management System**
This database manages **students, courses, professors, enrollments, departments, exams, and results**.  

---

## **📑 Table Structures & Data to Insert**  

### **1️⃣ Students Table** (📌 **Primary Key: student_id**)  
Stores student details.  

| student_id | student_name  | email                | phone      | city         |  
|------------|--------------|----------------------|------------|-------------|  
| 1          | John Doe     | john@example.com     | 9876543210 | New York    |  
| 2          | Alice Smith  | alice@example.com    | 9123456789 | London      |  
| 3          | Bob Brown    | bob@example.com      | 9988776655 | Paris       |  
| 4          | Emma Wilson  | emma@example.com     | 8899776655 | Berlin      |  
| 5          | Michael Lee  | michael@example.com  | 7766554433 | Toronto     |  

---

### **2️⃣ Departments Table** (📌 **Primary Key: dept_id**)  
Stores department details.  

| dept_id | dept_name      |  
|---------|--------------|  
| 1       | Computer Science |  
| 2       | Mathematics  |  
| 3       | Physics      |  
| 4       | Literature   |  
| 5       | History      |  

---

### **3️⃣ Professors Table** (📌 **Primary Key: professor_id, Foreign Key: dept_id**)  
Stores professor details.  

| professor_id | professor_name | email              | dept_id |  
|-------------|---------------|--------------------|---------|  
| 1           | Dr. Alan Turing | alan@uni.edu      | 1       |  
| 2           | Dr. Marie Curie | marie@uni.edu     | 3       |  
| 3           | Dr. Isaac Newton | newton@uni.edu   | 2       |  
| 4           | Dr. William Shakespeare | william@uni.edu | 4       |  
| 5           | Dr. John Keats | keats@uni.edu     | 5       |  

---

### **4️⃣ Courses Table** (📌 **Primary Key: course_id, Foreign Key: professor_id**)  
Stores course details.  

| course_id | course_name           | professor_id |  
|-----------|----------------------|--------------|  
| 101       | Data Structures       | 1            |  
| 102       | Calculus              | 3            |  
| 103       | Quantum Physics       | 2            |  
| 104       | Shakespearean Drama   | 4            |  
| 105       | World History         | 5            |  

---

### **5️⃣ Enrollments Table** (📌 **Primary Key: enrollment_id, Foreign Keys: student_id, course_id**)  
Stores which students are enrolled in which courses.  

| enrollment_id | student_id | course_id | grade |  
|--------------|-----------|----------|-------|  
| 1            | 1         | 101      | A     |  
| 2            | 2         | 102      | B+    |  
| 3            | 3         | 103      | A-    |  
| 4            | 4         | 104      | B     |  
| 5            | 5         | 105      | A+    |  
| 6            | 1         | 102      | B     |  
| 7            | 2         | 101      | A-    |  
| 8            | 3         | 105      | B+    |  
| 9            | 4         | 103      | A     |  
| 10           | 5         | 104      | B-    |  

---

### **6️⃣ Exams Table** (📌 **Primary Key: exam_id, Foreign Key: course_id**)  
Stores exam details.  

| exam_id | course_id | exam_date  | total_marks |  
|---------|----------|------------|-------------|  
| 1       | 101      | 2024-05-10 | 100         |  
| 2       | 102      | 2024-05-12 | 100         |  
| 3       | 103      | 2024-05-15 | 100         |  
| 4       | 104      | 2024-05-18 | 100         |  
| 5       | 105      | 2024-05-20 | 100         |  

---

### **7️⃣ Results Table** (📌 **Primary Key: result_id, Foreign Keys: student_id, exam_id**)  
Stores students’ exam results.  

| result_id | student_id | exam_id | obtained_marks |  
|----------|-----------|--------|---------------|  
| 1        | 1         | 1      | 85            |  
| 2        | 2         | 2      | 90            |  
| 3        | 3         | 3      | 78            |  
| 4        | 4         | 4      | 88            |  
| 5        | 5         | 5      | 92            |  

---

## **📝 Exam Questions (Each 2 Marks)**
**Section 1: Table Creation & Data Insertion**  
1. Create the **Students** table with a **Primary Key**.  
2. Create the **Departments** table and ensure `dept_name` is **unique**.  
3. Create the **Professors** table with a **Foreign Key** linking to `Departments`.  
4. Create the **Courses** table, ensuring `professor_id` is a **Foreign Key**.  
5. Create the **Enrollments** table with **Foreign Keys** referencing `Students` and `Courses`.  
6. Insert all **Students** data into the table.  
7. Insert all **Departments** data into the table.  
8. Insert all **Professors** data into the table.  
9. Insert all **Courses** data into the table.  
10. Insert all **Enrollments** data into the table.  

---

**Section 2: Data Retrieval Queries**  
11. Retrieve all students who live in "New York".  
12. Display all courses taught by "Dr. Alan Turing".  
13. Show all students enrolled in "Quantum Physics".  
14. Find professors who belong to the "Mathematics" department.  
15. Show the total number of students in each department.  
16. List students who have taken more than 2 courses.  
17. Retrieve details of students who received an "A" grade.  
18. Find courses with no enrollments.  
19. List all students along with their enrolled courses.  
20. Show total enrollments for each course.  

---

**Section 3: Aggregation & Analysis**  
21. Calculate the **average marks** obtained in each exam.  
22. Find students who scored above **90 marks**.  
23. Count the number of courses in each department.  
24. Show total **salary of all professors** (Assume a `salary` column).  
25. Retrieve the **highest grade** achieved in each course.  
26. Find the department with the **most professors**.  
27. Show students who scored below **50 marks**.  
28. List all professors who have more than **1 course**.  
29. Find students who have **never enrolled** in a course.  
30. Retrieve students who appeared in **all exams**.  

---

**Section 4: Foreign Key Constraints & Joins**  
31. Delete a **department** and observe what happens to professors.  
32. Try to delete a **student** and see how it affects enrollments.  
33. Update a **course name** and see if it affects enrollments.  
34. Change a **professor’s department** and check its effect.  
35. Attempt to insert an enrollment with a **non-existent student_id**.  