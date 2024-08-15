## 🔑 Why is a Primary Key Needed?

A **primary key** is essential in a database for several important reasons:

1. **Uniqueness**: The primary key ensures that each record in a table is unique. No two rows can have the same value for the primary key, which prevents duplicate records and maintains data integrity.

2. **Identification**: The primary key acts as a unique identifier for each record in the table. This makes it easy to reference and retrieve specific records quickly and efficiently.

3. **Indexing**: When a primary key is set, the database automatically creates an index on that column. This index significantly speeds up queries, especially those involving search operations.

4. **Relationships**: Primary keys are crucial for establishing relationships between tables. They serve as the basis for foreign keys in other tables, enabling the database to enforce referential integrity.

5. **Data Integrity**: By ensuring that each record is unique and can be reliably identified, primary keys help maintain the accuracy and consistency of the data within the database.

6. **Efficient Data Management**: Primary keys make it easier to update, delete, and manage records because each record can be precisely identified by its primary key value.

In summary, a primary key is a fundamental component of relational databases that ensures data integrity, supports efficient data retrieval, and establishes clear relationships between tables.


### Create table using id (primary key)
```sql
  - CREATE TABLE employee (
    id int,
    firstname VARCHAR(50) NOT NULL,
    secondname VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) NOT NULL DEFAULT 'bangalore'
  );
```

```
But above table can allow duplicate id, hence this is not acting as a primary key, so to make any column as primary key we need to specify it explicitly while creating table.
```

### Creating table using primary key
```sql
  - CREATE TABLE employee (
    id int PRIMARY KEY,
    firstname VARCHAR(50) NOT NULL,
    secondname VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) NOT NULL DEFAULT 'bangalore'
  );
```
Other way:
```sql
  - CREATE TABLE employee (
    id int,
    firstname VARCHAR(50) NOT NULL,
    secondname VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) NOT NULL DEFAULT 'bangalore',
    PRIMARY KEY(id)
  );
```

```
this will not allow duplicate id
```

**Inserting data**
```sql
INSERT INTO employee(id,firstname,secondname,lastname,age,salary,location) VALUES (123,'Praveen','Kumar','Srivas',28,100000,'Bangalore');
```
Inserting same data again:
```
ERROR 1062 (23000): Duplicate entry '123' for key 'employee.PRIMARY'
```
## 🔄 What is `AUTO_INCREMENT` in an SQL Table?

`AUTO_INCREMENT` is a feature in SQL used with a column to automatically generate a unique, sequential number whenever a new record is inserted into a table. This is commonly used for primary key columns where you want each record to have a unique identifier without manually specifying it.

### Key Points:

- **Automatic Increment**: When you insert a new record into a table, the `AUTO_INCREMENT` column automatically increases by 1 (or another specified increment) from the last highest value.
  
- **Primary Key Use**: It's often used for primary key columns because it ensures each row has a unique identifier.

- **Starting Value**: By default, the `AUTO_INCREMENT` starts at 1, but you can specify a different starting point if needed.

- **Database-Specific**: The exact syntax and behavior might vary slightly between different SQL databases (e.g., MySQL, PostgreSQL).

### Example:

Here's how you can create a table with an `AUTO_INCREMENT` column:

```sql
CREATE TABLE employees (
  id INT AUTO_INCREMENT PRIMARY KEY,
  firstname VARCHAR(50),
  lastname VARCHAR(50),
  age INT,
  salary INT,
  location varchar(20) NOT NULL DEFAULT 'bangalore'
);
```

```
desc employees;
+-----------+-------------+------+-----+-----------+----------------+
| Field     | Type        | Null | Key | Default   | Extra          |
+-----------+-------------+------+-----+-----------+----------------+
| id        | int         | NO   | PRI | NULL      | auto_increment |
| firstname | varchar(50) | YES  |     | NULL      |                |
| lastname  | varchar(50) | YES  |     | NULL      |                |
| age       | int         | YES  |     | NULL      |                |
| salary    | int         | YES  |     | NULL      |                |
| location  | varchar(20) | NO   |     | bangalore |                |
+-----------+-------------+------+-----+-----------+----------------+
```

***Inserting data***
  - INSERT INTO employees(firstname,lastname,age,salary,location) 
  VALUES ('Praveen','Srivas',28,100000,'Bangalore');
  - INSERT INTO employees(firstname,lastname,age,salary,location) 
  VALUES ('kapil','Sharma',36,120000,'Bangalore');

```
select * from employees;
+----+-----------+----------+------+--------+-----------+
| id | firstname | lastname | age  | salary | location  |
+----+-----------+----------+------+--------+-----------+
|  1 | Praveen   | Srivas   |   28 | 100000 | Bangalore |
|  2 | kapil     | Sharma   |   36 | 120000 | Bangalore |
+----+-----------+----------+------+--------+-----------+
2 rows in set (0.00 sec)
```

## 🔄 What is `IDENTITY` in an SQL Table?
```sql
CREATE TABLE employees (
  id INT IDENTITY(1,1) PRIMARY KEY,
  firstname VARCHAR(50),
  lastname VARCHAR(50),
  age INT,
  salary INT,
  location varchar(20) NOT NULL DEFAULT 'bangalore'
);
```
In this example, the id column is an identity column.
The seed value is 1, which means the first row inserted will have an id of 1.
The increment is also 1, so each subsequent row will have an id that increases by 1.

***Note:*** The terms IDENTITY and AUTO_INCREMENT refer to similar concepts in SQL, but they are used in different database management systems (DBMS) and have some differences in implementation. Here's a comparison:

## IDENTITY VS AUTO_INCREMENT:

| **Aspect**               | **IDENTITY** (SQL Server, Oracle, etc.)         | **AUTO_INCREMENT** (MySQL, MariaDB, etc.)          |
|--------------------------|-------------------------------------------------|----------------------------------------------------|
| **Usage**                | Primarily used in Microsoft SQL Server and Oracle (with specific settings). | Primarily used in MySQL and MariaDB.               |
| **Syntax**               | `IDENTITY(seed, increment)`                     | `AUTO_INCREMENT`                                   |
| **Example**              |                                          |                                             |
|                          | CREATE TABLE employees (                        | CREATE TABLE employees (                           |
|                          |     id INT IDENTITY(1,1) PRIMARY KEY,           |     id INT AUTO_INCREMENT PRIMARY KEY,             |
|                          |     name VARCHAR(100)                           |     name VARCHAR(100)                              |
|                          | );                                              | );                                               |
| **Seed Value**           | Specifies the starting value for the identity column. | The starting value is typically `1`, but can be customized. |
| **Increment**            | Specifies the step value for each new row.      | The value by which the identity increments (usually `1`, but can be customized). |
| **Default Behavior**     | Defaults to `IDENTITY(1,1)` if not specified.   | Defaults to `AUTO_INCREMENT` starting at `1` with an increment of `1`. |
| **Flexibility**          | Allows custom seed and increment values. Can retrieve the last inserted identity value using `SCOPE_IDENTITY()` or `@@IDENTITY`. | Allows setting custom starting value with the `AUTO_INCREMENT` keyword. Last inserted value can be retrieved using `LAST_INSERT_ID()`. |
| **Resetting**            | Can be reset using `DBCC CHECKIDENT`.           | Can be reset using `ALTER TABLE` with the `AUTO_INCREMENT` option. |
| **Database Support**     | Supported by SQL Server, Oracle (with special sequences), and some other RDBMS. | Supported by MySQL, MariaDB, and some other RDBMS. |
| **Limitations**          | Usually tied to specific databases like SQL Server; not portable across all RDBMS. | Specific to MySQL and MariaDB; less flexible in certain scenarios compared to sequences in Oracle. |
| **Concurrency Control**  | More robust in SQL Server for concurrent inserts. | May require careful handling in highly concurrent environments. |
---

## 🔑 What is a Unique Key in SQL?

A **unique key** is a database constraint that ensures all the values in a column (or a group of columns) are distinct across the entire table. This means that no two rows can have the same value(s) in the unique key column(s).

### Key Points:

- **Uniqueness**: The primary purpose of a unique key is to enforce the uniqueness of values in the column(s) it is applied to. This prevents duplicate values, helping to maintain data integrity.

- **Multiple Unique Keys**: A table can have multiple unique keys, unlike a primary key, where only one can exist per table.

- **NULL Values**: Unlike a primary key, a unique key can accept NULL values. However, depending on the database system, only one NULL value or more then one NULL values might be allowed per column.

- **Indexing**: When a unique key is defined on a column, the database often creates a unique index for faster query performance.

```sql
CREATE TABLE employees (
  id INT UNIQUE KEY,
  firstname VARCHAR(50),
  lastname VARCHAR(50),
  age INT NOT NULL
);
```

Insertng data
```sql
insert into employees values(1,'kapil','sharma',28);
```
Insertng again above data
```
ERROR 1062 (23000): Duplicate entry '1' for key 'employees.id'
```

Note: Hence Unique key does not allow duplicate key, But allow one or multiple NULL values
```sql
insert into employees values(NULL,'kapil','sharma',28);
insert into employees values(NULL,'babbal','jadu',78);
```
```
select * from employees;
+------+-----------+----------+-----+
| id   | firstname | lastname | age |
+------+-----------+----------+-----+
|    1 | kapil     | sharma   |  28 |
| NULL | kapil     | sharma   |  28 |
| NULL | babbal    | jadu     |  78 |
+------+-----------+----------+-----+
5 rows in set (0.01 sec)
```
#### Unique can be apply on combination of two cols
  - Example: 
```sql
          CREATE TABLE employees (
            id INT UNIQUE KEY,
            firstname VARCHAR(50),
            lastname VARCHAR(50),
            age INT NOT NULL,
            UNIQUE KEY(id,firstname)
          );
```

# Composite primary key:
This key will be combination of 2 columns

## Creating table with composite key
```sql
CREATE TABLE employee (
firstname VARCHAR(50) NOT NULL,
lastname VARCHAR(20) NOT NULL,
age INT NOT NULL,
primary key(firstname, lastname)
);
```
***Inserting the duplicate data***
```sql
Inserting the below data:
INSERT INTO employee 
VALUES ('Praveen','Kumar',28);

select * from employee;
+-----------+----------+-----+
| firstname | lastname | age |
+-----------+----------+-----+
| Praveen   | Kumar    |  28 |
+-----------+----------+-----+
```
Again isnerting the same data
```sql
INSERT INTO employee 
VALUES ('Praveen','Kumar',28);

ERROR 1062 (23000): Duplicate entry 'Praveen-Kumar' for key 'employee.PRIMARY'
```


## 🔑 Comparison of Primary Key, Unique Key, and Composite Key

| Feature/Aspect         | **Primary Key**                                              | **Unique Key**                                                | **Composite Key**                                               |
|------------------------|--------------------------------------------------------------|---------------------------------------------------------------|-----------------------------------------------------------------|
| **Definition**         | Uniquely identifies each record in a table                   | Ensures all values in the column(s) are unique                | A combination of two or more columns to uniquely identify a record |
| **Uniqueness**         | Yes, values must be unique                                   | Yes, values must be unique                                    | Yes, the combined values of the columns must be unique            |
| **NULL Values**        | Not allowed                                                  | Allowed (typically only one NULL per column)                  | Depends on the individual columns' constraints                   |
| **Number per Table**   | Only one primary key per table                               | Multiple unique keys can be defined in a table                | Multiple composite keys can be defined                          |
| **Indexing**           | Automatically indexed                                        | Automatically indexed                                         | Indexing depends on how the composite key is defined            |
| **Purpose**            | Main identifier for records, establishes relationships       | Enforces uniqueness for data integrity                        | Uniquely identifies records using a combination of columns      |
| **Use Case Example**   | `id` in an `employees` table                                 | `email` in a `users` table                                    | `(firstname, lastname)` in a `persons` table                     |
| **Relationship with Other Keys** | Often referenced by foreign keys in other tables | Can also be referenced by foreign keys (though less common)   | Typically used for complex keys and relationships               |

### **Summary:**

- **Primary Key**: The primary key is the main identifier for records in a table, ensuring both uniqueness and the absence of NULL values. There can only be one primary key per table.
  
- **Unique Key**: A unique key also enforces uniqueness but allows NULL values. Multiple unique keys can exist in a table.

- **Composite Key**: A composite key is a combination of two or more columns that together uniquely identify a record. It is useful when no single column can uniquely identify a record on its own.

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
