
# 🚀 SQL Aggregate Functions & GROUP BY Clause

## 📊 Aggregate Functions in SQL

Aggregate functions in SQL are used to perform calculations on a set of values and return a single summary value. These functions are often used in conjunction with the `GROUP BY` clause to summarize data by specific groups.

### 🔍 Common Aggregate Functions:

- **`COUNT()`**: Returns the number of rows that match a specified condition.

### Examples:

1. **Total rows in the `employees` table:**
   ```sql
   SELECT COUNT(*) FROM students;
   ```

   Output:
   ```
   +----------+
   | count(*) |
   +----------+
   |        7 |
   +----------+
   ```

2. **Count distinct `student_company`:**
   ```sql
   SELECT COUNT(DISTINCT student_company) FROM students;
   ```

   Output:
   ```
   +---------------------------------+
   | count(DISTINCT student_company) |
   +---------------------------------+
   |                               3 |
   +---------------------------------+
   ```

3. **Count distinct `location` of students, with output column as `total_unique_locations`:**
   ```sql
   SELECT COUNT(DISTINCT location) AS total_unique_locations FROM students;
   ```

   Output:
   ```
   +------------------------+
   | total_unique_locations |
   +------------------------+
   |                      7 |
   +------------------------+
   ```

4. **Count students who joined in September (9th month):**
   ```sql
   SELECT COUNT(*) FROM students WHERE batch_date LIKE '%-09-%';
   ```

   Output:
   ```
   +----------+
   | count(*) |
   +----------+
   |        3 |
   +----------+
   ```

- **`GROUP BY`**: The `GROUP BY` clause in SQL is used to arrange identical data into groups. This clause is often used in conjunction with aggregate functions (e.g., `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`) to perform calculations on each group of data and return a single result per group.

### Examples:

1. **Count students by `source_of_joining`:**
   ```sql
   SELECT source_of_joining, COUNT(*) FROM students GROUP BY source_of_joining;
   ```

   Output:
   ```
   +-------------------+----------+
   | source_of_joining | count(*) |
   +-------------------+----------+
   | Online            |        4 |
   | Referral          |        2 |
   | Event             |        1 |
   +-------------------+----------+
   ```

2. **Count students by `location`:**
   ```sql
   SELECT location, COUNT(*) FROM students GROUP BY location;
   ```

   Output:
   ```
   +------------+----------+
   | location   | count(*) |
   +------------+----------+
   | Delhi      |        1 |
   | Mumbai     |        1 |
   | Hyderabad  |        1 |
   | Kolkata    |        1 |
   | Ahmedabad  |        1 |
   | Chandigarh |        1 |
   | Rajkot     |        1 |
   +------------+----------+
   ```

3. **Find the maximum years of experience by `source_of_joining`:**
   ```sql
   SELECT source_of_joining, MAX(years_of_exp) FROM students GROUP BY source_of_joining;
   ```

   Output:
   ```
   +-------------------+-------------------+
   | source_of_joining | MAX(years_of_exp) |
   +-------------------+-------------------+
   | Online            |                11 |
   | Referral          |                12 |
   | Event             |                 9 |
   +-------------------+-------------------+
   ```

4. **Find the average years of experience by `location`:**
   ```sql
   SELECT location, AVG(years_of_exp) FROM students GROUP BY location;
   ```

   Output:
   ```
   +------------+-------------------+
   | location   | AVG(years_of_exp) |
   +------------+-------------------+
   | Delhi      |           10.0000 |
   | Mumbai     |            8.0000 |
   | Hyderabad  |            9.0000 |
   | Kolkata    |            7.0000 |
   | Ahmedabad  |            6.0000 |
   | Chandigarh |           12.0000 |
   | Rajkot     |           11.0000 |
   +------------+-------------------+
   ```

## 📚 Summary
The `GROUP BY` clause in SQL is used to group rows that have the same values in specified columns into aggregated data. It is often used with aggregate functions like `COUNT()`, `SUM()`, `AVG()`, etc., to perform calculations on each group and return a single result per group.

Happy Querying! 🎉

---
### If you like this SQL series please leave a star ⭐ to the repository Happy Learning 
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
