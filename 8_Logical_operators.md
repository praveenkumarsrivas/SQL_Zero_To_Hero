
# 🔍 SQL Logical Operators: Practical Guide with Examples

Understanding logical operators in SQL is crucial for filtering and combining multiple conditions in queries. Using the `students` table below, this guide will explain how to effectively use logical operators like `AND`, `OR`, `NOT`, and more. We’ll also cover tricky interview questions to help solidify your knowledge.

## 📋 The `students` Table

| student_id | student_fname | student_lname | student_mname | student_email               | student_phone | student_alternate_phone | enrollment_date     | years_of_exp | selected_course | student_company   | batch_date | source_of_joining | location   |
|------------|---------------|---------------|---------------|-----------------------------|---------------|-------------------------|---------------------|--------------|-----------------|-------------------|------------|-------------------|------------|
| 1          | Virat         | Kohli         | NULL          | virat.kohli@example.com     | 9000012345    | 9000098765              | 2024-08-14 00:37:54 | 10           | 1               | Cricket Academy   | 2023-09-20 | Online            | Delhi      |
| 2          | Rohit         | Sharma        | NULL          | rohit.sharma@example.com    | 9100012345    | NULL                    | 2024-08-14 00:37:54 | 8            | 2               | Sports Management | 2023-10-05 | Referral          | Mumbai     |
| 3          | Shikhar       | Dhawan        | NULL          | shikhar.dhawan@example.com  | 9200123456    | NULL                    | 2024-08-14 00:37:54 | 9            | 3               | NULL              | 2023-09-15 | Event             | Hyderabad  |
| 4          | Ishant        | Sharma        | NULL          | ishant.sharma@example.com   | 9300012345    | 9300098765              | 2024-08-14 00:37:54 | 7            | 4               | NULL              | 2023-11-01 | Online            | Kolkata    |
| 5          | Jasprit       | Bumrah        | NULL          | jasprit.bumrah@example.com  | 9400012345    | NULL                    | 2024-08-14 00:37:54 | 6            | 1               | NULL              | 2023-10-20 | Online            | Ahmedabad  |
| 6          | Yuvraj        | Singh         | NULL          | yuvraj.singh@example.com    | 9500012345    | NULL                    | 2024-08-14 00:37:54 | 12           | 2               | Sports Club       | 2023-10-10 | Referral          | Chandigarh |
| 7          | Ravindra      | Jadeja        | NULL          | ravindra.jadeja@example.com | 9600012345    | NULL                    | 2024-08-14 00:37:58 | 11           | 3               | NULL              | 2023-09-25 | Online            | Rajkot     |

## 🔗 Logical Operators in SQL

### 1. `AND` Operator
- **Description**: Combines two or more conditions; returns rows where all conditions are `TRUE`.
- **Example**: Find students with more than 8 years of experience who joined the course through `Online`.
  ```sql
  SELECT student_fname, student_lname, years_of_exp, source_of_joining
  FROM students
  WHERE years_of_exp > 8 AND source_of_joining = 'Online';
  ```
- **Expected Output**:
  | student_fname | student_lname | years_of_exp | source_of_joining |
  |---------------|---------------|--------------|-------------------|
  | Virat         | Kohli         | 10           | Online            |
  | Ravindra      | Jadeja        | 11           | Online            |

### 2. `OR` Operator
- **Description**: Combines two or more conditions; returns rows where at least one condition is `TRUE`.
- **Example**: Find students who either have more than 10 years of experience or joined via `Referral`.
  ```sql
  SELECT student_fname, student_lname, years_of_exp, source_of_joining
  FROM students
  WHERE years_of_exp > 10 OR source_of_joining = 'Referral';
  ```
- **Expected Output**:
  | student_fname | student_lname | years_of_exp | source_of_joining |
  |---------------|---------------|--------------|-------------------|
  | Yuvraj        | Singh         | 12           | Referral          |
  | Ravindra      | Jadeja        | 11           | Online            |
  | Rohit         | Sharma        | 8            | Referral          |

### 3. `NOT` Operator
- **Description**: Negates a condition; returns rows where the condition is `FALSE`.
- **Example**: Find students who do not belong to `Cricket Academy`.
  ```sql
  SELECT student_fname, student_lname, student_company
  FROM students
  WHERE NOT student_company = 'Cricket Academy';
  ```
- **Expected Output**:
  | student_fname | student_lname | student_company   |
  |---------------|---------------|-------------------|
  | Rohit         | Sharma        | Sports Management |
  | Shikhar       | Dhawan        | NULL              |
  | Ishant        | Sharma        | NULL              |
  | Jasprit       | Bumrah        | NULL              |
  | Yuvraj        | Singh         | Sports Club       |
  | Ravindra      | Jadeja        | NULL              |

### 4. `BETWEEN` Operator
- **Description**: Filters values within a specified range.
- **Example**: Find students with `years_of_exp` between 8 and 10 years.
  ```sql
  SELECT student_fname, student_lname, years_of_exp
  FROM students
  WHERE years_of_exp BETWEEN 8 AND 10;
  ```
- **Expected Output**:
  | student_fname | student_lname | years_of_exp |
  |---------------|---------------|--------------|
  | Virat         | Kohli         | 10           |
  | Rohit         | Sharma        | 8            |
  | Shikhar       | Dhawan        | 9            |

### 5. `IN` Operator
- **Description**: Filters rows based on a list of values.
- **Example**: Find students who joined either from `Delhi`, `Mumbai`, or `Rajkot`.
  ```sql
  SELECT student_fname, student_lname, location
  FROM students
  WHERE location IN ('Delhi', 'Mumbai', 'Rajkot');
  ```
- **Expected Output**:
  | student_fname | student_lname | location |
  |---------------|---------------|----------|
  | Virat         | Kohli         | Delhi    |
  | Rohit         | Sharma        | Mumbai   |
  | Ravindra      | Jadeja        | Rajkot   |


# 🎯 SQL `CASE` Statement: A Detailed Example

The `CASE` statement in SQL is a powerful conditional expression that allows you to perform different actions based on specified conditions. It’s often used to create computed columns or to transform data based on certain logic.

## 📋 The `students` Table

Let's use the following `students` table as an example:

| student_id | student_fname | student_lname | student_mname | student_email               | student_phone | student_alternate_phone | enrollment_date     | years_of_exp | selected_course | student_company   | batch_date | source_of_joining | location   |
|------------|---------------|---------------|---------------|-----------------------------|---------------|-------------------------|---------------------|--------------|-----------------|-------------------|------------|-------------------|------------|
| 1          | Virat         | Kohli         | NULL          | virat.kohli@example.com     | 9000012345    | 9000098765              | 2024-08-14 00:37:54 | 10           | 1               | Cricket Academy   | 2023-09-20 | Online            | Delhi      |
| 2          | Rohit         | Sharma        | NULL          | rohit.sharma@example.com    | 9100012345    | NULL                    | 2024-08-14 00:37:54 | 8            | 2               | Sports Management | 2023-10-05 | Referral          | Mumbai     |
| 3          | Shikhar       | Dhawan        | NULL          | shikhar.dhawan@example.com  | 9200123456    | NULL                    | 2024-08-14 00:37:54 | 9            | 3               | NULL              | 2023-09-15 | Event             | Hyderabad  |
| 4          | Ishant        | Sharma        | NULL          | ishant.sharma@example.com   | 9300012345    | 9300098765              | 2024-08-14 00:37:54 | 7            | 4               | NULL              | 2023-11-01 | Online            | Kolkata    |
| 5          | Jasprit       | Bumrah        | NULL          | jasprit.bumrah@example.com  | 9400012345    | NULL                    | 2024-08-14 00:37:54 | 6            | 1               | NULL              | 2023-10-20 | Online            | Ahmedabad  |
| 6          | Yuvraj        | Singh         | NULL          | yuvraj.singh@example.com    | 9500012345    | NULL                    | 2024-08-14 00:37:54 | 12           | 2               | Sports Club       | 2023-10-10 | Referral          | Chandigarh |
| 7          | Ravindra      | Jadeja        | NULL          | ravindra.jadeja@example.com | 9600012345    | NULL                    | 2024-08-14 00:37:58 | 11           | 3               | NULL              | 2023-09-25 | Online            | Rajkot     |

## 🔄 Using `CASE` to Categorize Students by Experience

### Example 1: Categorizing Experience Levels

We want to categorize students into three experience levels based on their `years_of_exp`:
- **Junior**: 0-5 years
- **Mid-Level**: 6-10 years
- **Senior**: 11+ years

### Query:
```sql
SELECT 
    student_fname, 
    student_lname, 
    years_of_exp,
    CASE 
        WHEN years_of_exp BETWEEN 0 AND 5 THEN 'Junior'
        WHEN years_of_exp BETWEEN 6 AND 10 THEN 'Mid-Level'
        WHEN years_of_exp >= 11 THEN 'Senior'
        ELSE 'Unknown'
    END AS experience_level
FROM students;
```

  | student_fname | student_lname | years_of_exp | experience_level |
  |---------------|---------------|--------------|------------------|
  | Virat         | Kohli         |           10 | Mid-Level        |
  | Rohit         | Sharma        |            8 | Mid-Level        |
  | Shikhar       | Dhawan        |            9 | Mid-Level        |
  | Ishant        | Sharma        |            7 | Mid-Level        |
  | Jasprit       | Bumrah        |            6 | Mid-Level        |
  | Yuvraj        | Singh         |           12 | Senior           |
  | Ravindra      | Jadeja        |           11 | Senior           |
  -------------------------------------------------------------------

###  Example 2: Determining Joining Source and Location
Let’s categorize students based on their source of joining and location. We want to:
- Label students from Online and Referral sources in Delhi or Mumbai as `"Priority Target"`.
- Label others as `"General Target"`.
```sql
select student_fname, student_lname,location,
CASE
  WHEN source_of_joining IN('Online','Referral')
    AND location IN("Mumbai","Delhi") then 'Priority Target'
  ELSE 'General Target'
END AS Target_Type
FROM students;
```
| student_fname | student_lname | location   | Target_Type     |
|---------------|---------------|------------|-----------------|
| Virat         | Kohli         | Delhi      | Priority Target |
| Rohit         | Sharma        | Mumbai     | Priority Target |
| Shikhar       | Dhawan        | Hyderabad  | General Target  |
| Ishant        | Sharma        | Kolkata    | General Target  |
| Jasprit       | Bumrah        | Ahmedabad  | General Target  |
| Yuvraj        | Singh         | Chandigarh | General Target  |
| Ravindra      | Jadeja        | Rajkot     | General Target  |
---




## 💡 Tricky Interview Questions & Tips

### 1. **How does the `AND` operator affect query performance?**
- **Explanation**: The `AND` operator narrows down the result set by combining multiple conditions, which may improve performance by reducing the number of rows returned. However, if the conditions are not indexed, it can slow down the query.

### 2. **What’s the difference between `NOT IN` and `NOT EXISTS`?**
- **Explanation**: `NOT IN` compares a value to a list of values and can be inefficient with large lists or when dealing with `NULL` values. `NOT EXISTS` is generally more efficient and is used in subqueries to exclude rows based on a condition.

### 3. **Can you combine `AND`, `OR`, and `NOT` in a single query?**
- **Explanation**: Yes, you can combine these operators, but be mindful of operator precedence. SQL evaluates `NOT` first, then `AND`, and finally `OR`. Use parentheses to control the evaluation order:
  ```sql
  SELECT student_fname, student_lname
  FROM students
  WHERE (years_of_exp > 10 OR source_of_joining = 'Referral') AND NOT location = 'Delhi';
  ```

## 🔗 Summary

Logical operators in SQL (`AND`, `OR`, `NOT`, `BETWEEN`, `IN`) are powerful tools for filtering data based on complex conditions. Mastering their use is key to writing efficient and effective SQL queries. Practice these operators with real-world examples to build your confidence! 💪


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
