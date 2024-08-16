
# 📊 SQL `ROW_NUMBER()` Function: A Detailed Explanation

The `ROW_NUMBER()` function in SQL is a powerful tool that assigns a unique sequential integer to rows within a result set. This function is often used for tasks like pagination, ranking, or simply numbering the rows in a specific order.

## 📚 Understanding `ROW_NUMBER()`

### Purpose
The `ROW_NUMBER()` function generates a unique number for each row in the result set, starting at 1. This numbering is determined by the order specified in the `ORDER BY` clause of the `OVER` function.

### Syntax
```sql
ROW_NUMBER() OVER (
    [PARTITION BY column_name(s)]
    ORDER BY column_name(s)
)
```

### Components
- **`ROW_NUMBER()`**: The function that generates the row number.
- **`OVER`**: Specifies the window of rows to which the function is applied.
- **`PARTITION BY`** (optional): Divides the result set into partitions, and the row number resets for each partition.
- **`ORDER BY`**: Determines the order in which the row numbers are assigned.

## 🧑‍💻 Practical Examples

### Example 1: Simple Use of `ROW_NUMBER()`

Let’s consider a table `employee` with the following columns:
```sql
+-----------+----------+------+---------+-----------+
| firstname | lastname | age  | salary  | location  |
+-----------+----------+------+---------+-----------+
| Virat     | Kohli    |   32 |  120000 | Delhi     |
| Rohit     | Sharma   |   34 |  110000 | Mumbai    |
| MS        | Dhoni    |   39 |  150000 | Ranchi    |
| Jasprit   | Bumrah   |   27 |   90000 | Ahmedabad |
| KL        | Rahul    |   29 |   85000 | Bangalore |
| Ravindra  | Jadeja   |   32 |   95000 | Rajkot    |
| Shikhar   | Dhawan   |   35 |  100000 | Delhi     |
| Hardik    | Pandya   |   27 |   95000 | Baroda    |
| Jam       | Khattar  |   42 |  145000 | Bangalore |
| Jacky     | Bhalla   |   56 | 1980000 | Ranchi    |
+-----------+----------+------+---------+-----------+
```

#### Find the 5th highest salary from employee table.
- First we will find the row_rank and then will make that table contating the row rank as temp table and we will select the 5th highest salary.
```sql
select * from (select firstname,lastname,salary, ROW_NUMBER() over (order by salary desc) as salary_rank from employee) as temptable where salary_rank=5;

+-----------+----------+--------+-------------+
| firstname | lastname | salary | salary_rank |
+-----------+----------+--------+-------------+
| Rohit     | Sharma   | 110000 |           5 |
+-----------+----------+--------+-------------+
```
#### Assign the row number for partition based on each location


```sql
select firstname,lastname,location,salary, ROW_NUMBER() over (partition by location order by salary desc) as location_wise_salary_rank from employee;

+-----------+----------+-----------+---------+---------------------------+
| firstname | lastname | location  | salary  | location_wise_salary_rank |
+-----------+----------+-----------+---------+---------------------------+
| Jasprit   | Bumrah   | Ahmedabad |   90000 |                         1 |
| Jam       | Khattar  | Bangalore |  145000 |                         1 |
| KL        | Rahul    | Bangalore |   85000 |                         2 |
| Hardik    | Pandya   | Baroda    |   95000 |                         1 |
| Virat     | Kohli    | Delhi     |  120000 |                         1 |
| Shikhar   | Dhawan   | Delhi     |  100000 |                         2 |
| Rohit     | Sharma   | Mumbai    |  110000 |                         1 |
| Ravindra  | Jadeja   | Rajkot    |   95000 |                         1 |
| Jacky     | Bhalla   | Ranchi    | 1980000 |                         1 |
| MS        | Dhoni    | Ranchi    |  150000 |                         2 |
+-----------+----------+-----------+---------+---------------------------+

MEANS: Bangalore is 2 times hence 1st rank is given to Jam khattar and 2nd rank given to KL Rahul in salary rank.
```
#### Find out the persons based on Location-wise highest salary.
```sql
select * from (select firstname,lastname,location,salary, ROW_NUMBER() over (partition by location order by salary desc) as location_wise_salary_rank from employee) as temptable where location_wise_salary_rank=1;

+-----------+----------+-----------+---------+---------------------------+
| firstname | lastname | location  | salary  | location_wise_salary_rank |
+-----------+----------+-----------+---------+---------------------------+
| Jasprit   | Bumrah   | Ahmedabad |   90000 |                         1 |
| Jam       | Khattar  | Bangalore |  145000 |                         1 |
| Hardik    | Pandya   | Baroda    |   95000 |                         1 |
| Virat     | Kohli    | Delhi     |  120000 |                         1 |
| Rohit     | Sharma   | Mumbai    |  110000 |                         1 |
| Ravindra  | Jadeja   | Rajkot    |   95000 |                         1 |
| Jacky     | Bhalla   | Ranchi    | 1980000 |                         1 |
+-----------+----------+-----------+---------+---------------------------+
```

## 🔑 Key Takeaways

- **`ROW_NUMBER()`**: Assigns a unique sequential number to each row in the result set, must required order by also partition by is optional.
- **`OVER` Clause**: Defines the window of rows over which the `ROW_NUMBER()` function operates.
- **`PARTITION BY` Clause**: (Optional) Divides the result set into partitions, resetting the row number for each partition.
- **Common Uses**: Pagination, ranking, ordering results.

---

##### Problem with ROW_NUMBER(): If we have duplicates in the Data then we will end up with wrong result if we want to fetch the particular row number for example:
```sql
select *,ROW_NUMBER() over (order by salary desc) as row_num from employee;
+-----------+----------+------+---------+-----------+---------+
| firstname | lastname | age  | salary  | location  | row_num |
+-----------+----------+------+---------+-----------+---------+
| Jacky     | Bhalla   |   56 | 1980000 | Ranchi    |       1 |
| MS        | Dhoni    |   39 |  150000 | Ranchi    |       2 |
| Jam       | Khattar  |   42 |  145000 | Bangalore |       3 |
| Virat     | Kohli    |   32 |  120000 | Delhi     |       4 |
| Jake      | Pol      |   31 |  120000 | Jind      |       5 |
| Baake     | Singh    |   30 |  120000 | Mumbai    |       6 |
| Rohit     | Sharma   |   34 |  110000 | Mumbai    |       7 |
| Shikhar   | Dhawan   |   35 |  100000 | Delhi     |       8 |
| Alam      | khan     |   45 |  100000 | Mumbai    |       9 |
| Ravindra  | Jadeja   |   32 |   95000 | Rajkot    |      10 |
| Hardik    | Pandya   |   27 |   95000 | Baroda    |      11 |
| Jasprit   | Bumrah   |   27 |   90000 | Ahmedabad |      12 |
| KL        | Rahul    |   29 |   85000 | Bangalore |      13 |
+-----------+----------+------+---------+-----------+---------+
```
Now we can see salary at row_num 4,5,6 all three are same salary but still they have different row_num as we have made the row_num based on the salary only, Hence the problem is that we will not get the exact 4th highest salary, ideally it should give all three as 4th highest salary

- To handle such problem we will have `RANK` and `DENSE RANK` concept in SQL.

## RANK and DENSE RANK:
#### Now let's run the above query again to check the results for RANK.
```sql
select *,RANK() over (order by salary desc) as row_num from employee;
+-----------+----------+------+---------+-----------+---------+
| firstname | lastname | age  | salary  | location  | row_num |
+-----------+----------+------+---------+-----------+---------+
| Jacky     | Bhalla   |   56 | 1980000 | Ranchi    |       1 |
| MS        | Dhoni    |   39 |  150000 | Ranchi    |       2 |
| Jam       | Khattar  |   42 |  145000 | Bangalore |       3 |
| Virat     | Kohli    |   32 |  120000 | Delhi     |       4 |
| Jake      | Pol      |   31 |  120000 | Jind      |       4 |
| Baake     | Singh    |   30 |  120000 | Mumbai    |       4 |
| Rohit     | Sharma   |   34 |  110000 | Mumbai    |       7 |
| Shikhar   | Dhawan   |   35 |  100000 | Delhi     |       8 |
| Alam      | khan     |   45 |  100000 | Mumbai    |       8 |
| Ravindra  | Jadeja   |   32 |   95000 | Rajkot    |      10 |
| Hardik    | Pandya   |   27 |   95000 | Baroda    |      10 |
| Jasprit   | Bumrah   |   27 |   90000 | Ahmedabad |      12 |
| KL        | Rahul    |   29 |   85000 | Bangalore |      13 |
+-----------+----------+------+---------+-----------+---------+
```
- Note: We have got the row_num same to same salary but if we check that after 4th row_num we do not have 5th row_num as it skips which is also cause problem some time.
- To overcome from this issue we have concept of `DENSE RANK`

#### Now let's run the above query again to check the results for  DENSE_RANK.
```sql
select *,DENSE_RANK() over (order by salary desc) as row_num from employee;

+-----------+----------+------+---------+-----------+---------+
| firstname | lastname | age  | salary  | location  | row_num |
+-----------+----------+------+---------+-----------+---------+
| Jacky     | Bhalla   |   56 | 1980000 | Ranchi    |       1 |
| MS        | Dhoni    |   39 |  150000 | Ranchi    |       2 |
| Jam       | Khattar  |   42 |  145000 | Bangalore |       3 |
| Virat     | Kohli    |   32 |  120000 | Delhi     |       4 |
| Jake      | Pol      |   31 |  120000 | Jind      |       4 |
| Baake     | Singh    |   30 |  120000 | Mumbai    |       4 |
| Rohit     | Sharma   |   34 |  110000 | Mumbai    |       5 |
| Shikhar   | Dhawan   |   35 |  100000 | Delhi     |       6 |
| Alam      | khan     |   45 |  100000 | Mumbai    |       6 |
| Ravindra  | Jadeja   |   32 |   95000 | Rajkot    |       7 |
| Hardik    | Pandya   |   27 |   95000 | Baroda    |       7 |
| Jasprit   | Bumrah   |   27 |   90000 | Ahmedabad |       8 |
| KL        | Rahul    |   29 |   85000 | Bangalore |       9 |
+-----------+----------+------+---------+-----------+---------+
```
- Note: Now we have proper row_num based on salary and we can see that which salary falls under which rank.



# 🏅 `RANK()` and `DENSE_RANK()` in SQL: Definitions and Use Cases


## 📊 `RANK()` Function

### Definition
The `RANK()` function assigns a unique rank to each row within a partition of the result set. The rank is determined by the order specified in the `ORDER BY` clause. If there are ties (i.e., rows with the same values in the order column), `RANK()` will assign the same rank to all those rows, but the next rank will skip as many numbers as there were ties.

### Use Case
- **Use Case**: Ranking students by their scores in a course. If two students have the same score, they get the same rank, but the next rank is skipped.

---`

## 📊 `DENSE_RANK()` Function

### Definition
The `DENSE_RANK()` function assigns a unique rank to each row within a partition of the result set, based on the order specified in the `ORDER BY` clause. Unlike the `RANK()` function, `DENSE_RANK()` does not skip any ranks when there are ties. This means that if multiple rows share the same value in the order column, they will receive the same rank, and the next rank will be the immediate subsequent number.

### Key Characteristics
- **No Gaps**: The ranking sequence is continuous, without gaps, even when there are ties.
- **Ties**: Rows with the same value in the order column receive the same rank.

### Use Case
- **Use Case**: Ranking employees by their salaries. When two or more employees have the same salary, they receive the same rank, and the following rank is the next consecutive number, without skipping any ranks.



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
