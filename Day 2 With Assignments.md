## **A. Database Operations (DDL)**

1. **Create Database:**  
   Write a MySQL query to create a database named `InventoryDB`.

2. **Use Database:**  
   After creating `InventoryDB`, write a query to switch to it.

3. **Drop Database:**  
   Write a MySQL query to drop the database `OldDB` if it exists.

---

## **B. Table Creation (DDL)**

4. **Products Table:**  
   Create a `products` table with the following columns:  
   - `product_id` INT AUTO_INCREMENT PRIMARY KEY  
   - `product_name` VARCHAR(100) NOT NULL  
   - `price` DECIMAL(10,2) DEFAULT 0.00  
   - `stock` INT DEFAULT 0

5. **Customers Table with UNIQUE Email:**  
   Create a `customers` table with:  
   - `customer_id` INT AUTO_INCREMENT PRIMARY KEY  
   - `customer_name` VARCHAR(100) NOT NULL  
   - `email` VARCHAR(100) NOT NULL UNIQUE

6. **Orders Table:**  
   Create an `orders` table with:  
   - `order_id` INT AUTO_INCREMENT PRIMARY KEY  
   - `customer_id` INT NOT NULL  
   - `order_date` DATE NOT NULL

7. **Order Items Table:**  
   Create an `order_items` table with:  
   - `item_id` INT AUTO_INCREMENT PRIMARY KEY  
   - `order_id` INT NOT NULL  
   - `product_id` INT NOT NULL  
   - `quantity` INT DEFAULT 1

8. **Suppliers Table with UNIQUE Contact:**  
   Create a `suppliers` table with:  
   - `supplier_id` INT AUTO_INCREMENT PRIMARY KEY  
   - `supplier_name` VARCHAR(100) NOT NULL  
   - `contact_number` VARCHAR(15) UNIQUE

9. **Categories Table with UNIQUE Category Name:**  
   Create a `categories` table with:  
   - `category_id` INT AUTO_INCREMENT PRIMARY KEY  
   - `category_name` VARCHAR(50) NOT NULL UNIQUE

10. **Reviews Table with CHECK Constraint:**  
    Create a `reviews` table with:  
    - `review_id` INT AUTO_INCREMENT PRIMARY KEY  
    - `product_id` INT NOT NULL  
    - `review_text` TEXT  
    - `rating` INT CHECK(rating >= 1 AND rating <= 5)

11. **Employees Table with UNIQUE Email:**  
    Create an `employees` table with:  
    - `emp_id` INT AUTO_INCREMENT PRIMARY KEY  
    - `name` VARCHAR(100) NOT NULL  
    - `email` VARCHAR(100) NOT NULL UNIQUE  
    - `salary` DECIMAL(10,2) DEFAULT 50000

---

## **C. Data Manipulation (DML)**

12. **Insert Multiple Products:**  
    Write a MySQL query to insert three records into the `products` table in one statement.

13. **Insert a Customer:**  
    Insert a record into the `customers` table with all required fields (ensure the email is unique).

14. **Insert an Order:**  
    Write a query to insert an order into the `orders` table, providing `customer_id` and `order_date`.

15. **Insert Multiple Order Items:**  
    Write a query to insert multiple rows into the `order_items` table in a single statement.

16. **Update Product Stock:**  
    Write a query to update the `stock` value of a product in the `products` table where `product_id` equals a specified value.

17. **Delete Low-Rated Review:**  
    Write a query to delete a review from the `reviews` table where the `rating` is below 3.

18. **Insert an Employee:**  
    Insert an employee record into the `employees` table with provided details.

---

## **D. Data Querying (DQL)**

19. **Select All Products:**  
    Write a MySQL query to select all columns from the `products` table.

20. **Select Specific Customer Details:**  
    Write a query to select `customer_name` and `email` from the `customers` table.

21. **Select Recent Orders:**  
    Write a query to fetch orders from the `orders` table that were placed in the current year.

22. **Select Products with High Stock:**  
    Write a query to select product names and prices from the `products` table where `stock` is greater than 10.

---

## **E. Table Alterations and Data Management**

23. **Add Discount Column:**  
    Write a MySQL query to add a new column `discount` (DECIMAL(5,2) DEFAULT 0.00) to the `products` table.

24. **Modify Customer Email Length:**  
    Write a query to modify the `email` column in the `customers` table to allow up to 150 characters.

25. **Drop Supplier Contact Column:**  
    Write a query to drop the `contact_number` column from the `suppliers` table.

26. **Rename Order Date Column:**  
    Write a query to rename the column `order_date` to `date_ordered` in the `orders` table.

27. **Rename Employees Table:**  
    Write a query to rename the `employees` table to `staff`.

28. **Truncate Order Items Table:**  
    Write a query to truncate the `order_items` table (remove all records but keep its structure).

29. **Update Review Rating:**  
    Write a query to update the `rating` in the `reviews` table for a given `review_id`.

30. **Delete Low-Salary Employees:**  
    Write a query to delete all records from the `staff` table where `salary` is below 40000.
