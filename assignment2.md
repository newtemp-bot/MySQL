### **1. Create Database**
1. Create a new database named `ecommerce_data`.
2. Show the list of databases after creating `ecommerce_data`.
3. Select and use the `ecommerce_data` database for all further operations.
4. Drop the `ecommerce_data` database.

---

### **2. Create Tables**

#### **Table: `customers_info`**
**Description:**
This table stores information about customers, including their ID, name, contact details, and registration date.

| Column Name    | Data Type      | Constraints       | Description                          |
|----------------|----------------|-------------------|--------------------------------------|
| `customer_id`  | INT            | PRIMARY KEY, AUTO_INCREMENT | Unique customer ID                |
| `customer_name`| VARCHAR(100)   | NOT NULL          | Customer's name                     |
| `contact_number`| VARCHAR(15)    |                   | Customer's contact number           |
| `email`        | VARCHAR(100)   |                   | Customer's email address            |
| `reg_date`     | DATE           |                   | Date of customer registration       |

#### **Table: `product_inventory`**
**Description:**
This table stores information about products in an inventory, including their ID, name, category, price, and stock quantity.

| Column Name    | Data Type      | Constraints       | Description                          |
|----------------|----------------|-------------------|--------------------------------------|
| `product_id`   | INT            | PRIMARY KEY, AUTO_INCREMENT | Unique product ID                |
| `product_name` | VARCHAR(100)   | NOT NULL          | Name of the product                 |
| `category`     | VARCHAR(50)    |                   | Category of the product             |
| `price`        | DECIMAL(10,2)  |                   | Price of the product                |
| `stock_qty`    | INT            |                   | Quantity of the product in stock    |

1. Create the `customers_info` table with the specified columns and constraints.
2. Create the `product_inventory` table with the specified columns and constraints.
3. Show all the tables in the `ecommerce_data` database.
4. Describe the `product_inventory` table to view its structure.

---

### **3. Alter Table**

1. Add a new column `shipping_address` (VARCHAR) to the `customers_info` table.
2. Modify the `price` column in the `product_inventory` table to increase the length to `DECIMAL(12,2)`.
3. Drop the `shipping_address` column from the `customers_info` table.
4. Rename the `category` column to `product_category` in the `product_inventory` table.

---

### **4. Inserting Data**

1. Insert a record into the `customers_info` table with sample values for `customer_name`, `contact_number`, `email`, and `reg_date`.
2. Insert multiple records into the `product_inventory` table, including different products with their prices and stock quantities.
3. Insert a record into the `customers_info` table, leaving the `email` column empty.
4. Insert a record into the `product_inventory` table for a product with `stock_qty` set to 0.

---

### **5. Selecting Data**

1. Select all fields from the `customers_info` table.
2. Select only the `customer_name` and `contact_number` columns from the `customers_info` table.
3. Select all customers who registered after `2023-01-01`.
4. Select all products with a `price` greater than 50.
5. Select distinct product categories from the `product_inventory` table.

---

### **6. Updating and Deleting Data**

1. Update the `contact_number` of a customer with a specific `customer_id`.
2. Delete a product from the `product_inventory` table by `product_id`.
3. Update the `email` for a customer with a specific `customer_id`.
4. Delete all records from the `product_inventory` table where `stock_qty` is 0.

---

### **7. Ordering and Grouping Data**

1. Order the customers by `reg_date` in ascending order.
2. Group the customers by `reg_date` and count how many customers registered each month.
3. Order the products by `price` in descending order.
4. Group the products by `product_category` and find the total number of products in each category.
