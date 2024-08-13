
## CRUD in SQL 🛠️

**CRUD** is an acronym defining the main tasks that can be performed on relational databases. In SQL, CRUD operations are the foundation that facilitates database development. CRUD stands for the following:

- **CREATE** means adding or inserting rows into a table.
- **READ** means selecting (retrieving) rows from a table.
- **UPDATE** means modifying rows in a table.
- **DELETE** means removing rows from a table.

All these operations come under DML (Data Manipulation Language).

### 🌟 Create Operations

Let's create a table **EMPLOYEE** for demonstration:

- **Steps to create a database:**
  ```sql
  CREATE DATABASE praveen;
  ```

- **Get into the database:**
  ```sql
  USE praveen;
  ```

- **Create the EMPLOYEE table:**
  ```sql
  CREATE TABLE employee(
    id INT PRIMARY KEY,
    firstname VARCHAR(20) NOT NULL,
    midlename VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) NOT NULL DEFAULT 'bangalore'
  );
  ```

- **Insert records:**
  ```sql
  INSERT INTO employee(id, firstname, lastname, age, salary) 
  VALUES(1, 'Praveen', 'Srivas', 28, 100000);
  INSERT INTO employee(id, firstname, lastname, age, salary) 
  VALUES(2, 'Jake', 'Pol', 33, 120000);
  INSERT INTO employee(id, firstname, lastname, age, salary) 
  VALUES(3, 'Rubi', 'Raj', 38, 140000);
  SELECT * FROM employee;
  ```

### 📘 Read the Data

- **Fetch specific columns (e.g., firstname and lastname) from the EMPLOYEE table:**
  ```sql
  SELECT firstname, lastname FROM employee;
  ```

- **Fetch columns where the person's age is greater than 30:**
  ```sql
  SELECT * FROM employee WHERE age > 30;
  ```

### ✏️ Update the Table

- **Update the lastname of Rubi from Raj to Sinha:**
  ```sql
  UPDATE employee SET lastname = 'Sinha' WHERE firstname = 'Rubi';
  ```

- **Update the location of Jake from Bangalore to Hyderabad:**
  ```sql
  UPDATE employee SET location = 'Hyderabad' WHERE firstname = 'Jake';
  ```

- **Increase salary by 5000 for all employees:**
  ```sql
  UPDATE employee SET salary = salary + 5000;
  ```

### ❌ Delete Operations

- **Delete the record whose id is 3:**
  ```sql
  DELETE FROM employee WHERE id = 3;
  ```

- **Delete all records in the table:**
  ```sql
  DELETE FROM employee;
  ```

This tutorial covers all CRUD operations and how they fit into SQL's Data Manipulation Language (DML).


# DDL (Data Definition Language)
Purpose: Defines the structure and schema of the database.
Operations: Includes commands like CREATE, ALTER, DROP, and TRUNCATE.
Alter use to alter the table, means altering the schema.

### Adding column using Alter 
- Alter the employee table to add column jobtitle
```sql
alter table employee add column jobtitle varchar(50);

+-----------+-------------+------+-----+-----------+-------+
| Field     | Type        | Null | Key | Default   | Extra |
+-----------+-------------+------+-----+-----------+-------+
| id        | int         | NO   | PRI | NULL      |       |
| firstname | varchar(20) | NO   |     | NULL      |       |
| midlename | varchar(20) | YES  |     | NULL      |       |
| lastname  | varchar(20) | NO   |     | NULL      |       |
| age       | int         | NO   |     | NULL      |       |
| salary    | int         | NO   |     | NULL      |       |
| location  | varchar(20) | NO   |     | bangalore |       |
| jobtitle  | varchar(50) | YES  |     | NULL      |       |
+-----------+-------------+------+-----+-----------+-------+
```

### Drop column using alter
- Drop the employee table column jobtitle
```sql
Alter table employee drop column jobtitle;

+-----------+-------------+------+-----+-----------+-------+
| Field     | Type        | Null | Key | Default   | Extra |
+-----------+-------------+------+-----+-----------+-------+
| id        | int         | NO   | PRI | NULL      |       |
| firstname | varchar(20) | NO   |     | NULL      |       |
| midlename | varchar(20) | YES  |     | NULL      |       |
| lastname  | varchar(20) | NO   |     | NULL      |       |
| age       | int         | NO   |     | NULL      |       |
| salary    | int         | NO   |     | NULL      |       |
| location  | varchar(20) | NO   |     | bangalore |       |
+-----------+-------------+------+-----+-----------+-------+
```

- If we want to increase the length of the firstname column to accept longer lengths
  To do this we need `modify` to perform this action on the table
```sql
alter table employee modify column firstname varchar(30);

+-----------+-------------+------+-----+-----------+-------+
| Field     | Type        | Null | Key | Default   | Extra |
+-----------+-------------+------+-----+-----------+-------+
| id        | int         | NO   | PRI | NULL      |       |
| firstname | varchar(30) | YES  |     | NULL      |       |
| midlename | varchar(20) | YES  |     | NULL      |       |
| lastname  | varchar(20) | NO   |     | NULL      |       |
| age       | int         | NO   |     | NULL      |       |
| salary    | int         | NO   |     | NULL      |       |
| location  | varchar(20) | NO   |     | bangalore |       |
+-----------+-------------+------+-----+-----------+-------+
```

## Dropping Primary key
Here we have id as a primary key, now if we drop the primary key the id column will remain in the table but the uniqueness of id (for each row) will get removed and duplicate ids can be inserted into the table.

```sql
alter table employee drop primary key;

+-----------+-------------+------+-----+-----------+-------+
| Field     | Type        | Null | Key | Default   | Extra |
+-----------+-------------+------+-----+-----------+-------+
| id        | int         | NO   |     | NULL      |       |
| firstname | varchar(30) | YES  |     | NULL      |       |
| midlename | varchar(20) | YES  |     | NULL      |       |
| lastname  | varchar(20) | NO   |     | NULL      |       |
| age       | int         | NO   |     | NULL      |       |
| salary    | int         | NO   |     | NULL      |       |
| location  | varchar(20) | NO   |     | bangalore |       |
+-----------+-------------+------+-----+-----------+-------+
```
***Note:*** if we want to make id as the primary key again, we can do this using the `add` keyword.
```sql
alter table employee add primary key(id);

+-----------+-------------+------+-----+-----------+-------+
| Field     | Type        | Null | Key | Default   | Extra |
+-----------+-------------+------+-----+-----------+-------+
| id        | int         | NO   | PRI | NULL      |       |
| firstname | varchar(30) | YES  |     | NULL      |       |
| midlename | varchar(20) | YES  |     | NULL      |       |
| lastname  | varchar(20) | NO   |     | NULL      |       |
| age       | int         | NO   |     | NULL      |       |
| salary    | int         | NO   |     | NULL      |       |
| location  | varchar(20) | NO   |     | bangalore |       |
+-----------+-------------+------+-----+-----------+-------+
```

### Truncate table
**TRUNCATE**: Quickly removes all rows from a table without logging individual row deletions, but it cannot be rolled back in most cases and resets identity columns.
***Key Points:***
- Table Structure: The table structure, along with its columns, indexes, and constraints, remains intact after a TRUNCATE. Only the data within the table is removed.
- Identity Columns: If the table has an identity column, TRUNCATE resets the identity seed back to its initial value.
- Triggers and Constraints: Triggers are not fired during a TRUNCATE, but constraints (such as foreign keys) are still enforced.

```sql
truncate table employee;

select * from employee;
Empty set
```
---
### Truncate vs Delete
| **Aspect**            | **DELETE**                                             | **TRUNCATE**                                       |
|-----------------------|--------------------------------------------------------|----------------------------------------------------|
| **Purpose**           | Removes specific rows from a table.                    | Removes all rows from a table.                     |
| **Where Clause**      | Can use a `WHERE` clause to delete specific rows.      | Cannot use a `WHERE` clause; deletes all rows.     |
| **Logging**           | Row-by-row deletion; each row deletion is logged.      | Minimal logging, usually faster than `DELETE`.     |
| **Triggers**          | Triggers associated with the table will be fired.      | Triggers do not fire when using `TRUNCATE`.        |
| **Rollback**          | Can be rolled back (transaction safe).                 | Cannot be rolled back in most cases.               |
| **Effect on Table**   | Does not reset identity columns.                       | Resets identity columns to the seed value.         |
| **Performance**       | Generally slower for large datasets.                   | Generally faster for large datasets.               |

---
# DDL vs DML

| **Aspect**           | **DDL (Data Definition Language)**                   | **DML (Data Manipulation Language)**                    |
|----------------------|------------------------------------------------------|--------------------------------------------------------|
| **Purpose**          | Defines the structure and schema of the database.    | Manipulates and manages the data within the database.   |
| **Operations**       | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`                | `SELECT`, `INSERT`, `UPDATE`, `DELETE`                 |
| **Effect**           | Alters the schema and structure of database objects. | Affects the data within the database.                  |
| **Example Command**  | `CREATE TABLE employees (...);`                      | `INSERT INTO employees (...);`                         |


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