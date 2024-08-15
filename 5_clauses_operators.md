# SQL Query Components

In SQL, the terms **`DISTINCT`**, **`ORDER BY`**, **`LIMIT`**, and **`LIKE`** can be categorized as **"clauses"** or **"operators"** based on their functionality:

## Clauses
- **`ORDER BY`**: A clause used to define the sorting order of the returned data. It sorts the data in ascending (`ASC`) or descending (`DESC`) order based on one or more columns.
- **`LIMIT`**: A clause that specifies the maximum number of records to return from the top of the result set. Commonly used for pagination.

## Operators
- **`DISTINCT`**: An operator used in a `SELECT` statement to return only unique values in the result set, eliminating duplicates.
- **`LIKE`**: An operator used for pattern matching within a `WHERE` clause. It can be used with wildcards such as `%` (zero, one, or multiple characters) and `_` (a single character).

# Examples: 
## 1. Distinct
- Taking the reference of `STUDENTS` table, find out the distinct location from students
```sql
select DISTINCT location from students;

+------------+
| location   |
+------------+
| Delhi      |
| Mumbai     |
| Hyderabad  |
| Kolkata    |
| Ahmedabad  |
| Chandigarh |
| Rajkot     |
+------------+
```
- Find out the distinct student_company from students
```sql
select DISTINCT student_company from students;

+-------------------+
| student_company   |
+-------------------+
| Cricket Academy   |
| Sports Management |
| NULL              |
| Sports Club       |
+-------------------+
```

## 2. Order By (By default Ascending order)
- If we want the data in order by years_of_exp
```sql
select student_id, enrollment_date,selected_course, student_fname, years_of_exp, student_company, batch_date, source_of_joining, location from students ORDER BY  years_of_exp;

+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
| student_id | enrollment_date     | selected_course | student_fname | years_of_exp | student_company   | batch_date | source_of_joining | location   |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
|          5 | 2024-08-14 00:37:54 |               1 | Jasprit       |            6 | NULL              | 2023-10-20 | Online            | Ahmedabad  |
|          4 | 2024-08-14 00:37:54 |               4 | Ishant        |            7 | NULL              | 2023-11-01 | Online            | Kolkata    |
|          2 | 2024-08-14 00:37:54 |               2 | Rohit         |            8 | Sports Management | 2023-10-05 | Referral          | Mumbai     |
|          3 | 2024-08-14 00:37:54 |               3 | Shikhar       |            9 | NULL              | 2023-09-15 | Event             | Hyderabad  |
|          1 | 2024-08-14 00:37:54 |               1 | Virat         |           10 | Cricket Academy   | 2023-09-20 | Online            | Delhi      |
|          7 | 2024-08-14 00:37:58 |               3 | Ravindra      |           11 | NULL              | 2023-09-25 | Online            | Rajkot     |
|          6 | 2024-08-14 00:37:54 |               2 | Yuvraj        |           12 | Sports Club       | 2023-10-10 | Referral          | Chandigarh |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
```

- If we want the student_fname in order by years_of_exp
```sql
select student_fname,years_of_exp from students ORDER BY years_of_exp;

+---------------+--------------+
| student_fname | years_of_exp |
+---------------+--------------+
| Jasprit       |            6 |
| Ishant        |            7 |
| Rohit         |            8 |
| Shikhar       |            9 |
| Virat         |           10 |
| Ravindra      |           11 |
| Yuvraj        |           12 |
+---------------+--------------+
```
- If we want the student_fname in order by years_of_exp in descending order
```sql
select student_fname,years_of_exp from students ORDER BY years_of_exp desc;

+---------------+--------------+
| student_fname | years_of_exp |
+---------------+--------------+
| Yuvraj        |           12 |
| Ravindra      |           11 |
| Virat         |           10 |
| Shikhar       |            9 |
| Rohit         |            8 |
| Ishant        |            7 |
| Jasprit       |            6 |
+---------------+--------------+
```

- if we want to order by student_fname with year_of _exp we will use column name or column number as below

```sql
select student_fname,years_of_exp from students ORDER BY student_fname desc;
or
select student_fname,years_of_exp from students ORDER BY 1 desc; (Note:  student_fname is column number1 and year_of_exp is the column number 2 in this query)
 
+---------------+--------------+
| student_fname | years_of_exp |
+---------------+--------------+
| Yuvraj        |           12 |
| Virat         |           10 |
| Shikhar       |            9 |
| Rohit         |            8 |
| Ravindra      |           11 |
| Jasprit       |            6 |
| Ishant        |            7 |
+---------------+--------------+
```

### what if we give 2 columns in `ORDER BY` ?
- When you use two columns in the ORDER BY clause in SQL, the query sorts the results based on the first column specified, and then within those sorted results, it further sorts them based on the second column. This allows for a more refined sorting order

***EXAMPLE:***
```sql
select student_fname,years_of_exp from students ORDER BY student_fname,years_of_exp;
```
- Detailed Breakdown:
  - Primary Sorting: The data is first sorted by the student_fname column. All entries in the same student_fname are grouped together in the result set.
  - Secondary Sorting: Within each student_fname group, the data is then sorted by years_of_exp. If the first sorting criterion (student_fname) results in a tie, the second criterion (years_of_exp) determines the order of those specific rows.

##### Note: below table is dummy table not related to above data (This is just for understanding purpose)
***Students Sorted by Name and Years of Experience***

```sql
+---------------+--------------+
| student_fname | years_of_exp |
+---------------+--------------+
| Alice         | 1            |
| Alice         | 3            |
| Bob           | 2            |
| Charlie       | 0            |
| Charlie       | 5            |
| Dave          | 2            |
| Emma          | 4            |
+---------------+--------------+

in above table there is tie in Alice hence the sorting done based on years_of_exp
```

# Limit
- Suppose we want the top 3 students of least experienced
```sql
select student_id, enrollment_date,selected_course, student_fname, years_of_exp, student_company, batch_date, source_of_joining, location from students order by years_of_exp limit 3;

+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+-----------+
| student_id | enrollment_date     | selected_course | student_fname | years_of_exp | student_company   | batch_date | source_of_joining | location  |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+-----------+
|          5 | 2024-08-14 00:37:54 |               1 | Jasprit       |            6 | NULL              | 2023-10-20 | Online            | Ahmedabad |
|          4 | 2024-08-14 00:37:54 |               4 | Ishant        |            7 | NULL              | 2023-11-01 | Online            | Kolkata   |
|          2 | 2024-08-14 00:37:54 |               2 | Rohit         |            8 | Sports Management | 2023-10-05 | Referral          | Mumbai    |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+-----------+
```

- Suppose we want the top 3 students of maximum experienced
```sql
select student_id, enrollment_date,selected_course, student_fname, years_of_exp, student_company, batch_date, source_of_joining, location from students order by years_of_exp desc limit 3;

+------------+---------------------+-----------------+---------------+--------------+-----------------+------------+-------------------+------------+
| student_id | enrollment_date     | selected_course | student_fname | years_of_exp | student_company | batch_date | source_of_joining | location   |
+------------+---------------------+-----------------+---------------+--------------+-----------------+------------+-------------------+------------+
|          6 | 2024-08-14 00:37:54 |               2 | Yuvraj        |           12 | Sports Club     | 2023-10-10 | Referral          | Chandigarh |
|          7 | 2024-08-14 00:37:58 |               3 | Ravindra      |           11 | NULL            | 2023-09-25 | Online            | Rajkot     |
|          1 | 2024-08-14 00:37:54 |               1 | Virat         |           10 | Cricket Academy | 2023-09-20 | Online            | Delhi      |
+------------+---------------------+-----------------+---------------+--------------+-----------------+------------+-------------------+------------+
```


- Suppose we want to know from which source_of_joining last 5 candidates have enrolled?
```sql
select source_of_joining from students order by enrollment_date desc limit 5;
+-------------------+
| source_of_joining |
+-------------------+
| Online            |
| Online            |
| Referral          |
| Event             |
| Online            |
+-------------------+
```

- Suppose we want to know last candidate who has joined
```sql
select student_fname from students order by enrollment_date desc limit 1;
+---------------+
| student_fname |
+---------------+
| Ravindra      |
+---------------+
```

- Suppose we want to know last candidate who has joined
```sql
select student_fname from students order by enrollment_date desc limit 1;
+---------------+
| student_fname |
+---------------+
| Ravindra      |
+---------------+
```

- Suppose we want to get the records from the table order by enrollment_date but skip the first 3 rows and show next 2 records means show only 4th,5th record (count start from 0 instead 1)
```sql
select student_id, enrollment_date,selected_course, student_fname, years_of_exp, student_company, batch_date, source_of_joining, location from students order by enrollment_date limit 3,2;
+------------+---------------------+-----------------+---------------+--------------+-----------------+------------+-------------------+-----------+
| student_id | enrollment_date     | selected_course | student_fname | years_of_exp | student_company | batch_date | source_of_joining | location  |
+------------+---------------------+-----------------+---------------+--------------+-----------------+------------+-------------------+-----------+
|          4 | 2024-08-14 00:37:54 |               4 | Ishant        |            7 | NULL            | 2023-11-01 | Online            | Kolkata   |
|          5 | 2024-08-14 00:37:54 |               1 | Jasprit       |            6 | NULL            | 2023-10-20 | Online            | Ahmedabad |
+------------+---------------------+-----------------+---------------+--------------+-----------------+------------+-------------------+-----------+
```
***Understanding `LIMIT 3,2`*** 

- **`3`** - This number represents the offset. It tells SQL to skip the first three rows in the result set.
- **`2`** - This number is the count. After skipping the first three rows, the query retrieves the next two rows.


## LIKE
- Suppose we want to know the student_fname who have `kh` in his/her name
```sql
select student_id,selected_course, student_fname, years_of_exp, batch_date, source_of_joining, location from students where student_fname LIKE '%kh%';

+------------+-----------------+---------------+--------------+------------+-------------------+-----------+
| student_id | selected_course | student_fname | years_of_exp | batch_date | source_of_joining | location  |
+------------+-----------------+---------------+--------------+------------+-------------------+-----------+
|          3 |               3 | Shikhar       |            9 | 2023-09-15 | Event             | Hyderabad |
+------------+-----------------+---------------+--------------+------------+-------------------+-----------+
```

- Suppose we want to know the student_fname who have `ro` in begining of his/her name
```sql
select student_id,selected_course, student_fname, years_of_exp, batch_date, source_of_joining, location from students where student_fname LIKE 'ro%';

+------------+-----------------+---------------+--------------+------------+-------------------+----------+
| student_id | selected_course | student_fname | years_of_exp | batch_date | source_of_joining | location |
+------------+-----------------+---------------+--------------+------------+-------------------+----------+
|          2 |               2 | Rohit         |            8 | 2023-10-05 | Referral          | Mumbai   |
+------------+-----------------+---------------+--------------+------------+-------------------+----------+
```

- Suppose we want to know the student_fname who have `aj` in end of his/her name
```sql
select student_id,selected_course, student_fname, years_of_exp, batch_date, source_of_joining, location from students where student_fname LIKE '%aj';

+------------+-----------------+---------------+--------------+------------+-------------------+------------+
| student_id | selected_course | student_fname | years_of_exp | batch_date | source_of_joining | location   |
+------------+-----------------+---------------+--------------+------------+-------------------+------------+
|          6 |               2 | Yuvraj        |           12 | 2023-10-10 | Referral          | Chandigarh |
+------------+-----------------+---------------+--------------+------------+-------------------+------------+
```

- Suppose we want to know the student_fname who have exactly 5 letters in his/her name (we will use 5 underscore _)
```sql
select student_id,selected_course, student_fname, years_of_exp, batch_date, source_of_joining, location from students where student_fname LIKE '_____';
+------------+-----------------+---------------+--------------+------------+-------------------+----------+
| student_id | selected_course | student_fname | years_of_exp | batch_date | source_of_joining | location |
+------------+-----------------+---------------+--------------+------------+-------------------+----------+
|          1 |               1 | Virat         |           10 | 2023-09-20 | Online            | Delhi    |
|          2 |               2 | Rohit         |            8 | 2023-10-05 | Referral          | Mumbai   |
+------------+-----------------+---------------+--------------+------------+-------------------+----------+
```


### Why DISTINCT does not work with ORDER BY with different column
***Example:***
```sql
select DISTINCT source_of_joining from students ORDER BY enrollment_date desc;
```
  - ERROR 3065 (HY000): Expression #1 of ORDER BY clause is not in SELECT list, references column 'cs_portal.students.enrollment_date' which is not in SELECT list; this is incompatible with DISTINCT

#### REASON:
Taking the above query:
```sql
select DISTINCT source_of_joining from students ORDER BY enrollment_date desc;
```
When we give the Distinct with one column (source_of_joining) and order by with different column (enrollment_date) then the DISTINCT try to apply on both the column i.e. source_of_joining and enrollment_date which gives diffrent number of distinct result such as 3 distinct records  with source_of_joining and 5 distinct with enrollment_date and this causes bad results or non-consistent results hence SQL will not allow this kind of operation to be happen.


#### Fun fact, DISTINCT can work with similary column with ORDER BY
```sql
select DISTINCT source_of_joining from students ORDER BY source_of_joining desc;

+-------------------+
| source_of_joining |
+-------------------+
| Referral          |
| Online            |
| Event             |
+-------------------+
```
***REASON:***
This is because Distinct will perform his ction on only one column there is no other column to deal with it.


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