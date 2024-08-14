
# 📊 SQL Data Types: A Comprehensive Guide with Examples and some useful tips

Understanding data types in SQL is essential for defining the kind of data that can be stored in a table. Each column in a database table is required to have a data type that specifies the type of data that can be stored in that column. Here’s a guide to SQL data types, along with examples and some tricky interview questions to help you ace your next SQL interview!

## 🔢 Numeric Data Types

### 1. `INT` (Integer)
- **Description**: Stores whole numbers without decimals.
- **Example**: Age of a person.
  ```sql
  CREATE TABLE employees (
      employee_id INT,
      age INT
  );
  ```
- **Expected Output**: When you insert a value like `INSERT INTO employees (employee_id, age) VALUES (1, 25);`, the `age` column will store `25` as an integer.

### 2. `DECIMAL` (Fixed-point)
- **Description**: Stores numbers with a fixed number of decimal places.
- **Example**: Storing monetary values like salary.
  ```sql
  CREATE TABLE salaries (
      salary DECIMAL(10, 2)
  );
  ```
- **Expected Output**: If you insert `INSERT INTO salaries (salary) VALUES (12345.678);`, it will store `12345.68` because of the precision defined as `DECIMAL(10, 2)`.

### 3. `FLOAT` and `DOUBLE` (Floating-point)
- **Description**: Stores approximate numeric values with floating decimal points.
- **Example**: Scientific calculations or measurements.
  ```sql
  CREATE TABLE measurements (
      temperature FLOAT,
      distance DOUBLE
  );
  ```
- **Expected Output**: Values like `temperature = 98.6` or `distance = 123.456789` will be stored with floating precision, which may cause slight rounding.

## 🗓 Date and Time Data Types

### 1. `DATE`
- **Description**: Stores date values (Year, Month, Day).
- **Example**: Birthdate of an employee.
  ```sql
  CREATE TABLE employees (
      employee_id INT,
      birthdate DATE
  );
  ```
- **Expected Output**: Inserting `INSERT INTO employees (employee_id, birthdate) VALUES (1, '1990-01-01');` will store the date as `1990-01-01`.

### 2. `TIME`
- **Description**: Stores time values (Hours, Minutes, Seconds).
- **Example**: Record the time an employee clocks in.
  ```sql
  CREATE TABLE work_schedule (
      employee_id INT,
      clock_in TIME
  );
  ```
- **Expected Output**: Inserting `INSERT INTO work_schedule (employee_id, clock_in) VALUES (1, '08:30:00');` will store the time as `08:30:00`.

### 3. `DATETIME` and `TIMESTAMP`
- **Description**: Stores date and time information.
- **Example**: Timestamp for transaction records.
  ```sql
  CREATE TABLE transactions (
      transaction_id INT,
      transaction_time TIMESTAMP
  );
  ```
- **Expected Output**: Inserting `INSERT INTO transactions (transaction_id, transaction_time) VALUES (1, '2024-01-01 10:00:00');` will store the value as `2024-01-01 10:00:00`.

## 💬 String Data Types

### 1. `CHAR` (Fixed-length)
- **Description**: Stores fixed-length character strings.
- **Example**: Storing a fixed-length code like 'A123'.
  ```sql
  CREATE TABLE products (
      product_code CHAR(5)
  );
  ```
- **Expected Output**: Inserting `INSERT INTO products (product_code) VALUES ('A1');` will store it as `'A1   '` (padded with spaces).

### 2. `VARCHAR` (Variable-length)
- **Description**: Stores variable-length character strings.
- **Example**: Names or addresses.
  ```sql
  CREATE TABLE customers (
      customer_name VARCHAR(100)
  );
  ```
- **Expected Output**: Inserting `INSERT INTO customers (customer_name) VALUES ('John Doe');` will store it exactly as `'John Doe'` without padding.

### 3. `TEXT`
- **Description**: Stores large amounts of text data.
- **Example**: Product descriptions, comments.
  ```sql
  CREATE TABLE reviews (
      review_text TEXT
  );
  ```
- **Expected Output**: Can store long text such as `INSERT INTO reviews (review_text) VALUES ('This is a very detailed review...');`.

## 🔗 Binary Data Types

### 1. `BLOB` (Binary Large Object)
- **Description**: Stores binary data, such as images or files.
- **Example**: Storing profile pictures.
  ```sql
  CREATE TABLE user_profiles (
      user_id INT,
      profile_picture BLOB
  );
  ```
- **Expected Output**: Binary data like images will be stored as a series of bytes.

## ✅ Boolean Data Types

### 1. `BOOLEAN`
- **Description**: Stores TRUE or FALSE values.
- **Example**: Flags indicating if a user is active.
  ```sql
  CREATE TABLE users (
      user_id INT,
      is_active BOOLEAN
  );
  ```
- **Expected Output**: Storing `INSERT INTO users (user_id, is_active) VALUES (1, TRUE);` will store the value as `1` (for TRUE).

## 💡 Tricky Interview Questions & Tips

### 1. **How does SQL handle `NULL` values with aggregate functions?**
- **Explanation**: SQL aggregate functions like `SUM`, `AVG`, `COUNT` ignore `NULL` values in their calculations. For example:
  ```sql
  SELECT SUM(salary) FROM employees WHERE bonus IS NULL;
  ```
  This will sum only the `salary` values where `bonus` is `NULL`, ignoring any other rows.

### 2. **What’s the difference between `CHAR` and `VARCHAR`?**
- **Explanation**: `CHAR` is a fixed-length data type, meaning if the data is shorter than the specified length, it is padded with spaces. `VARCHAR` is variable-length, so it uses only as much space as needed for the data.
  ```sql
  -- Example
  CREATE TABLE example_table (
      fixed_char CHAR(5),
      variable_char VARCHAR(5)
  );
  ```
  - Inserting `'A1'` into `fixed_char` will store it as `'A1   '`.
  - Inserting `'A1'` into `variable_char` will store it as `'A1'`.

### 3. **How can `BLOB` be used to store files in a database?**
- **Explanation**: `BLOB` (Binary Large Object) is used to store binary data, such as images, audio, or any type of file, as a series of bytes.
  ```sql
  INSERT INTO user_profiles (user_id, profile_picture) VALUES (1, LOAD_FILE('/path/to/image.jpg'));
  ```
  - This will store the image file in the `profile_picture` column as binary data.

### 4. **What happens when you exceed the defined precision in a `DECIMAL` data type?**
- **Explanation**: If you exceed the precision, SQL rounds the value to the nearest possible value within the defined precision. 
  ```sql
  CREATE TABLE example_table (
      precise_value DECIMAL(5, 2)
  );
  INSERT INTO example_table (precise_value) VALUES (123.456);
  ```
  - The value `123.456` will be stored as `123.46`.

## 🔗 Summary

- **Numeric Types**: `INT`, `DECIMAL`, `FLOAT`, `DOUBLE` for numbers.
- **Date and Time Types**: `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` for temporal data.
- **String Types**: `CHAR`, `VARCHAR`, `TEXT` for text.
- **Binary Types**: `BLOB` for binary data.
- **Boolean Type**: `BOOLEAN` for true/false values.

Each data type serves a specific purpose, and understanding their intricacies is key to optimizing storage, performance, and handling edge cases effectively. Good luck with your SQL journey! 🚀

---
### If you like this SQL series of notes please leave a star ⭐ to the repository Happy Learning 
<img width="579" alt="image" src="https://github.com/user-attachments/assets/dd0ba111-f39c-4f4b-ae38-5ac30af30db9">
<p align="left">
    <a href="https://www.linkedin.com/in/praveennitk/">
        <img src="https://cdn-icons-png.flaticon.com/512/174/174857.png" width="20" alt="LinkedIn"> LinkedIn
    </a> |
    <a href="https://github.com/praveenkumarsrivas">
        <img src="https://cdn-icons-png.flaticon.com/512/25/25231.png" width="20" alt="GitHub"> GitHub
    </a> |
    <a href="https://www.instagram.com/me_prvn/">
        <img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width="20" alt="Instagram"> Instagram
    </a>
</p>
