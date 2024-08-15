## WHERE VS HAVING IN SQL:

In SQL, both the `WHERE` and `HAVING` clauses are used to filter data, but they serve different purposes and are used at different stages in the query process. Understanding the distinction between them is crucial for writing effective SQL queries.


## 📍 `WHERE` Clause

- **Purpose**: The `WHERE` clause is used to filter rows before any groupings are made. It is applied to each row in the table to determine whether it should be included in the result set.
- **Usage**: It is commonly used with `SELECT`, `UPDATE`, and `DELETE` statements.
- **Filtering**: Filters data at the row level, i.e., before aggregation occurs.

```Taking the resference of our students table```
```sql
SELECT student_fname, student_lname, years_of_exp
FROM students
WHERE years_of_exp > 8;

| student_fname | student_lname | years_of_exp |
|---------------|---------------|--------------|
| Virat         | Kohli         |           10 |
| Shikhar       | Dhawan        |            9 |
| Yuvraj        | Singh         |           12 |
| Ravindra      | Jadeja        |           11 |
|---------------|---------------|--------------|
```
---

## 📍 `HAVING` Clause
- **Purpose**: The HAVING clause is used to filter groups after the GROUP BY clause has been applied. It is typically used with aggregate functions.
- **Usage**:It is used after the GROUP BY clause in a SELECT statement.
- **Filtering**: Filters data at the group level, i.e., after aggregation has occurred.
### 🔑 Key Differences:

#### Order of Execution:
- **`WHERE`** is applied **before** `GROUP BY` and `HAVING`.
- **`HAVING`** is applied **after** `GROUP BY`.

#### Use Cases:
- **`WHERE`** is used for filtering rows **before** any aggregation.
- **`HAVING`** is used for filtering groups **after** aggregation.

#### Example Use:
- **`WHERE`** can filter based on conditions like `years_of_exp > 8`.
- **`HAVING`** can filter groups based on aggregate conditions like `COUNT(*) > 1`.

---

**Example:** Using the same students table, suppose we want to find selected_course with more than one student enrolled in the same course.
```sql
Select selected_course, count(*) as total_course_enrolled from students group by selected_course having count(*)>1;

+-----------------+-----------------------+
| selected_course | total_course_enrolled |
+-----------------+-----------------------+
|               1 |                     2 |
|               2 |                     2 |
|               3 |                     2 |
+-----------------+-----------------------+
```

### Question:
- 1. Fetch the lead source through which more then one person enrolled/registered.
  ```sql
  select source_of_joining,count(*) as total_enrolled from students group by source_of_joining;
  +-------------------+----------------+
  | source_of_joining | total_enrolled |
  +-------------------+----------------+
  | Online            |              4 |
  | Referral          |              2 |
  | Event             |              1 |
  +-------------------+----------------+
  ```

- 2. Fetch the lead source through which more then one person enrolled/registered more then 1 person
  ```sql
  select source_of_joining,count(*) as total_enrolled from students group by source_of_joining having total_enrolled>1;
  +-------------------+----------------+
  | source_of_joining | total_enrolled |
  +-------------------+----------------+
  | Online            |              4 |
  | Referral          |              2 |
  +-------------------+----------------+
  ```

- 3. Get all the students count registered through online 
  ```sql
  select source_of_joining,count(*) from students where source_of_joining = 'Online' group by source_of_joining;
  ```

### Can we use `WHERE` and `HAVING` clause simultaneously?
- ANS: Yes we can, below is the example.

Example: The location from which more than 1 student enrolled and student experience should be more than 10 years?

```sql
  select location, count(*) from students where years_of_exp>10 group by location having count(*)>1;

  Empty set (0.00 sec)
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
