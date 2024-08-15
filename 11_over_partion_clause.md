## To understand about the `OVER` AND `PARTITION` first we will create a table to get handson on it.
```sql
-- Create the employee table
CREATE TABLE employee (
    firstname VARCHAR(50),
    lastname VARCHAR(50),
    age INT,
    salary INT,
    location VARCHAR(50)
);

-- Insert data into the employee table with Indian cricketer names
INSERT INTO employee (firstname, lastname, age, salary, location) VALUES
('Virat', 'Kohli', 32, 120000, 'Delhi'),
('Rohit', 'Sharma', 34, 110000, 'Mumbai'),
('MS', 'Dhoni', 39, 150000, 'Ranchi'),
('Jasprit', 'Bumrah', 27, 90000, 'Ahmedabad'),
('KL', 'Rahul', 29, 85000, 'Bangalore'),
('Ravindra', 'Jadeja', 32, 95000, 'Rajkot'),
('Shikhar', 'Dhawan', 35, 100000, 'Delhi'),
('Hardik', 'Pandya', 27, 95000, 'Baroda');
```

INSERT INTO employee (firstname, lastname, age, salary, location) VALUES
('Jam', 'Khattar', 42, 145000, 'Bangalore'),
('Jacky', 'Bhalla', 56, 1980000, 'Ranchi')

# 🆚 `OVER` Clause vs `PARTITION BY` Clause in SQL

In SQL, the `OVER` and `PARTITION BY` clauses are closely related but serve different purposes when used with window functions. Understanding their differences and how they complement each other is crucial for writing effective SQL queries that involve complex calculations.

## 📍 `OVER` Clause

### Purpose
The `OVER` clause is used to define a window of rows within a query result set over which a window function (e.g., `ROW_NUMBER()`, `RANK()`, `SUM()`, `AVG()`) operates.

### Syntax
```sql
window_function() OVER (
    [PARTITION BY column_name(s)]
    [ORDER BY column_name(s)]
    [ROWS or RANGE frame_clause]
)
```

### Key Points
- **Defines the scope** of the window function.
- Can include `PARTITION BY`, `ORDER BY`, and `ROWS` or `RANGE` to refine how the function operates.
- **Without `PARTITION BY`**, the function operates on the entire result set.

### Example
```sql
SELECT 
    student_fname,
    student_lname,
    ROW_NUMBER() OVER (ORDER BY student_fname) AS row_num
FROM 
    students;
```

**Explanation**: This query assigns a row number to each student based on the alphabetical order of their first names across the entire dataset.

### Expected Output
| student_fname | student_lname | row_num |
|---------------|---------------|---------|
| Jasprit       | Bumrah        | 1       |
| Ravindra      | Jadeja        | 2       |
| KL            | Rahul         | 3       |
| Rohit         | Sharma        | 4       |
| Virat         | Kohli         | 5       |

## 📍 `PARTITION BY` Clause

### Purpose
The `PARTITION BY` clause is used within the `OVER` clause to divide the result set into partitions. The window function is then applied to each partition separately.

### Syntax
```sql
window_function() OVER (
    PARTITION BY column_name(s)
    [ORDER BY column_name(s)]
    [ROWS or RANGE frame_clause]
)
```

### Key Points
- **Divides the result set** into groups (partitions) based on the values of one or more columns.
- Each partition is processed separately by the window function.
- Often used to perform calculations within specific groups in the data.

### Example
```sql
SELECT 
    student_fname,
    student_lname,
    RANK() OVER (PARTITION BY selected_course ORDER BY years_of_exp DESC) AS rank
FROM 
    students;
```

**Explanation**: This query ranks students within each `selected_course` based on their `years_of_exp` in descending order.

### Expected Output
| student_fname | student_lname | selected_course | rank |
|---------------|---------------|-----------------|------|
| Virat         | Kohli         | 1               | 1    |
| Jasprit       | Bumrah        | 1               | 2    |
| Yuvraj        | Singh         | 2               | 1    |
| Rohit         | Sharma        | 2               | 2    |
| Ravindra      | Jadeja        | 3               | 1    |
| Shikhar       | Dhawan        | 3               | 2    |

## 🔑 Key Differences:

### 1. **Functionality**:
- **`OVER`**: Defines the entire window within which the function operates. It can include `PARTITION BY`, `ORDER BY`, and other clauses to refine the scope of the operation.
- **`PARTITION BY`**: Specifically divides the result set into partitions or groups. The function is applied separately to each partition.

### 2. **Scope of Operation**:
- **`OVER`**: Can be applied to the entire result set or to partitions created by the `PARTITION BY` clause.
- **`PARTITION BY`**: Limits the scope of the window function to specific partitions of the data, defined by the values of one or more columns.

### 3. **Use Cases**:
- **`OVER`**: Used when you need to perform calculations across the entire result set or within specified partitions.
- **`PARTITION BY`**: Used when you need to divide the data into groups and perform calculations separately within each group.

By understanding these differences, you can effectively use the `OVER` and `PARTITION BY` clauses to perform complex data analysis and reporting in SQL.
---



### Let's jump on some examples.
1. How many people are from each location and avg salary at each location
```sql
select location, count(location), avg(salary) from employee group by location;
+-----------+-----------------+--------------+
| location  | count(location) | avg(salary)  |
+-----------+-----------------+--------------+
| Delhi     |               2 |  110000.0000 |
| Mumbai    |               1 |  110000.0000 |
| Ranchi    |               2 | 1065000.0000 |
| Ahmedabad |               1 |   90000.0000 |
| Bangalore |               2 |  115000.0000 |
| Rajkot    |               1 |   95000.0000 |
| Baroda    |               1 |   95000.0000 |
+-----------+-----------------+--------------+
```
2. Show the firstname, lastname, location and it's count along with the avg salary for each user?
- Now we will try to frame the query and see waht we will get.
```sql
select firstname,lastname,location,count(location), avg(salary) from employee group by location;

ERROR 1140 (42000): In aggregated query without GROUP BY, expression #1 of SELECT list contains nonaggregated column 'cs_portal.employee.firstname'; this is incompatible with sql_mode=only_full_group_by
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'group by location' at line 1
```
- Now we are not able to do that because 2 column are invloved for result which required group by i.e. count(location), avg(salary) which is not possibel by above approach.
Hence we will split the query into two parts.
    - First we will find the results based on location and another based on salary
    ```sql
    select employee.firstname,employee.lastname, employee.location, total_count,avg_salary from employee
    join 
    (select location,count(location) as total_count,avg(salary) as avg_salary from employee group by location) temptable on employee.location = temptable.location;

    +-----------+----------+-----------+-------------+--------------+
    | firstname | lastname | location  | total_count | avg_salary   |
    +-----------+----------+-----------+-------------+--------------+
    | Virat     | Kohli    | Delhi     |           2 |  110000.0000 |
    | Rohit     | Sharma   | Mumbai    |           1 |  110000.0000 |
    | MS        | Dhoni    | Ranchi    |           2 | 1065000.0000 |
    | Jasprit   | Bumrah   | Ahmedabad |           1 |   90000.0000 |
    | KL        | Rahul    | Bangalore |           2 |  115000.0000 |
    | Ravindra  | Jadeja   | Rajkot    |           1 |   95000.0000 |
    | Shikhar   | Dhawan   | Delhi     |           2 |  110000.0000 |
    | Hardik    | Pandya   | Baroda    |           1 |   95000.0000 |
    | Jam       | Khattar  | Bangalore |           2 |  115000.0000 |
    | Jacky     | Bhalla   | Ranchi    |           2 | 1065000.0000 |
    +-----------+----------+-----------+-------------+--------------+
    ```

### Note: This above result can be achieved by using `OVER PARTITION BY` with minimal sql query.

```sql
select firstname,lastname,location,count(location) OVER (PARTITION BY location) as total, avg(salary) OVER (PARTITION BY location) as average from employee;
+-----------+----------+-----------+-------+--------------+
| firstname | lastname | location  | total | average      |
+-----------+----------+-----------+-------+--------------+
| Jasprit   | Bumrah   | Ahmedabad |     1 |   90000.0000 |
| KL        | Rahul    | Bangalore |     2 |  115000.0000 |
| Jam       | Khattar  | Bangalore |     2 |  115000.0000 |
| Hardik    | Pandya   | Baroda    |     1 |   95000.0000 |
| Virat     | Kohli    | Delhi     |     2 |  110000.0000 |
| Shikhar   | Dhawan   | Delhi     |     2 |  110000.0000 |
| Rohit     | Sharma   | Mumbai    |     1 |  110000.0000 |
| Ravindra  | Jadeja   | Rajkot    |     1 |   95000.0000 |
| MS        | Dhoni    | Ranchi    |     2 | 1065000.0000 |
| Jacky     | Bhalla   | Ranchi    |     2 | 1065000.0000 |
+-----------+----------+-----------+-------+--------------+
```



Happy querying! 🎉
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
