### **1. Create Database**
1. Create a new database named `company_records`.
2. Show the list of databases after creating `company_records`.
3. Select and use the `company_records` database for all further operations.
4. Drop the `company_records` database.

---

### **2. Create Tables**

#### **Table: `staff_members`**
**Description:**
This table stores information about the employees, including their ID, name, age, department, and joining date.

| Column Name   | Data Type     | Constraints       | Description                      |
|---------------|---------------|-------------------|----------------------------------|
| `staff_id`    | INT           | PRIMARY KEY, AUTO_INCREMENT | Unique staff ID               |
| `staff_name`  | VARCHAR(100)  | NOT NULL          | Staff member name               |
| `staff_age`   | INT           |                   | Age of the staff member         |
| `staff_dept`  | VARCHAR(50)   |                   | Department the staff works in   |
| `joining_date`| DATE          |                   | Date the staff joined the company|

#### **Table: `items_in_stock`**
**Description:**
This table stores information about items in a store, including their ID, name, price, and stock quantity.

| Column Name   | Data Type     | Constraints       | Description                      |
|---------------|---------------|-------------------|----------------------------------|
| `item_id`     | INT           | PRIMARY KEY, AUTO_INCREMENT | Unique item ID               |
| `item_name`   | VARCHAR(100)  | NOT NULL          | Name of the item                |
| `item_price`  | DECIMAL(10,2) |                   | Price of the item               |
| `item_stock`  | INT           |                   | Quantity of the item in stock   |

1. Create the `staff_members` table with the specified columns and constraints.
2. Create the `items_in_stock` table with the specified columns and constraints.
3. Show all the tables in the `company_records` database.
4. Describe the `staff_members` table to view its structure.

---

### **3. Alter Table**

1. Add a new column `contact_email` (VARCHAR) to the `staff_members` table.
2. Modify the `staff_age` column in the `staff_members` table to allow NULL values.
3. Drop the `contact_email` column from the `staff_members` table.
4. Rename the `item_name` column to `product_name` in the `items_in_stock` table.

---

### **4. Inserting Data**

1. Insert a record into the `staff_members` table with sample values for `staff_name`, `staff_age`, `staff_dept`, and `joining_date`.
2. Insert multiple records into the `items_in_stock` table, including different items with their prices and stock quantities.
3. Insert a record into the `staff_members` table, leaving the `staff_age` column empty.
4. Insert a record into the `items_in_stock` table for an item that has a `item_stock` of 0.

---

### **5. Selecting Data**

1. Select all fields from the `staff_members` table.
2. Select only the `staff_name` and `staff_age` columns from the `staff_members` table.
3. Select all staff members who are older than 30.
4. Select all items in stock that have a `item_price` greater than 100.
5. Select distinct departments from the `staff_members` table.

---

### **6. Updating and Deleting Data**

1. Update the `staff_age` of a staff member with a specific `staff_id`.
2. Delete an item from the `items_in_stock` table by `item_id`.
3. Update the `staff_dept` for a staff member with a specific `staff_id`.
4. Delete all records from the `items_in_stock` table where `item_stock` is 0.

---

### **7. Ordering and Grouping Data**

1. Order the staff members by `staff_age` in descending order.
2. Group the staff members by `staff_dept` and count how many staff members belong to each department.
3. Order the items by `item_price` in ascending order.
4. Group the items in stock by `item_stock` and find the total number of items with more than 100 units in stock.
