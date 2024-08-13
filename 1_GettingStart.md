# 🗄️ SQL Database Operations Cheat Sheet

## 🛠️ Create Database
```sql
CREATE DATABASE Database_name;
```

## 📂 Show Databases
```sql
SHOW DATABASES;
```

## 🔍 Select a Database
```sql
USE database_name;
```

## 📋 Create Table in Database
```sql
CREATE TABLE table_name (
  col1 datatype,
  col2 datatype
);
```

## 📝 Show Table Structure
```sql
DESC table_name;
```

## 🗑️ Drop Table
```sql
DROP TABLE table_name;
```
*NOTE:* To get into SQL db use ```mysql -u root -p```
---

## 🚀 Example: Creating an `employee` Table
```sql
CREATE TABLE employee (
  firstname VARCHAR(50),
  secondname VARCHAR(20),
  lastname VARCHAR(20),
  age INT,
  salary INT,
  location VARCHAR(20)
);
```

#### 📝 Note: We will use the above table for reference.

## 📊 Show Data
```sql
SELECT * FROM employee;
```

## ➕ Inserting Data into Table

- **1st way**: 
  ```sql
  INSERT INTO employee(firstname,secondname,lastname,age,salary,location) 
  VALUES ('Praveen','Kumar','Srivas',28,100000,'Bangalore');
  ```

- **2nd way**: 
  ```sql
  INSERT INTO employee 
  VALUES ('Praveen','Kumar','Srivas',28,100000,'Bangalore');
  ```

- **If no second name available**:
  ```sql
  INSERT INTO employee(firstname,lastname,age,salary,location) 
  VALUES('Don','Ji',32,7002300,'Delhi');
  ```

- **If we have `'` in name**:
  ```sql
  INSERT INTO employee 
  VALUES ("jame's",'Kumar','Srivas',28,100000,'Bangalore');
  ```
  or
  ```sql
  INSERT INTO employee 
  VALUES ('jame/'s','Kumar','Srivas',28,100000,'Bangalore');
  ```

## ➕ Inserting Multiple Rows
```sql
INSERT INTO employee(firstname,secondname,lastname,age,salary,location) 
VALUES 
('Ram','Ji','Sen',29,200000,'Bangalore'), 
('Jake','Pol','Khan',45,180000,'Bangalore');
```

## 🚫 Datatype Mismatch/Length Issue Error

- Example 1:
  ```sql
  INSERT INTO employee(firstname,secondname,lastname,age,salary,location) 
  VALUES 
  ('Hubert Blaine','Wolfeschlegelsteinhausenbergerdorff','Sr',45,2000200,'Bangalore');
  ```
  Error: `ERROR 1406 (22001): Data too long for column 'secondname' at row 1`

- Example 2:
  ```sql
  INSERT INTO employee 
  VALUES ('Praveen','Kumar','Srivas',32,'twenty lacs','Bangalore');
  ```
  Error: `ERROR 1366 (HY000): Incorrect integer value: 'twenty lacs' for column 'salary' at row 1`

## 🚫 Avoiding NULL in Mandatory Fields (Adding Constraints)

- If we need only the middle name to be null, all other fields should be mandatory:
  ```sql
  CREATE TABLE employee (
    firstname VARCHAR(50) NOT NULL,
    secondname VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) NOT NULL
  );
  ```

## 🚫 Inserting Data with Missing Mandatory Fields
```sql
INSERT INTO employee(secondname,lastname,age,salary,location) 
VALUES ('Kumar','Srivas',28,100000,'Bangalore');
```
Error: `ERROR 1364 (HY000): Field 'firstname' doesn't have a default value`

## 🌟 Default Values
- If we want to insert a default value when a value is not provided, we can define the default value while creating the table:
  ```sql
  CREATE TABLE employee (
    firstname VARCHAR(50) NOT NULL,
    secondname VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) DEFAULT 'Bangalore'
  );
  ```

## 📝 Table Structure
```sql
DESC employee;
+------------+-------------+------+-----+-----------+-------+
| Field      | Type        | Null | Key | Default   | Extra |
+------------+-------------+------+-----+-----------+-------+
| firstname  | VARCHAR(50) | NO   |     | NULL      |       |
| secondname | VARCHAR(20) | YES  |     | NULL      |       |
| lastname   | VARCHAR(20) | NO   |     | NULL      |       |
| age        | INT         | NO   |     | NULL      |       |
| salary     | INT         | NO   |     | NULL      |       |
| location   | VARCHAR(20) | YES  |     | Bangalore |       |
+------------+-------------+------+-----+-----------+-------+
```

## ➕ Inserting Data with Default Values
- **No location is given**:
  ```sql
  INSERT INTO employee(firstname,secondname,lastname,age,salary) 
  VALUES('Praveen','Kumar','Srivas',28,100000);
  ```

- **Location given other than Bangalore**:
  ```sql
  INSERT INTO employee(firstname,secondname,lastname,age,salary, location) 
  VALUES('Praveen','Kumar','Srivas',28,100000,'Mumbai');
  ```

- **Giving location NULL**:
  ```sql
  INSERT INTO employee(firstname,secondname,lastname,age,salary, location) 
  VALUES('Jake','Pol','Gupta',28,100000,NULL);
  ```

```sql
SELECT * FROM employee;
+-----------+------------+----------+-----+--------+-----------+
| firstname | secondname | lastname | age | salary | location  |
+-----------+------------+----------+-----+--------+-----------+
| Praveen   | Kumar      | Srivas   |  28 | 100000 | Bangalore |
| Praveen   | Kumar      | Srivas   |  28 | 100000 | Mumbai    |
| Jake      | Pol        | Gupta    |  28 | 100000 | NULL      |
+-----------+------------+----------+-----+--------+-----------+
```

## 🌟 Default Values Without NULL
- To ensure the default value is not null, set the location as NOT NULL:
  ```sql
  CREATE TABLE employee (
    firstname VARCHAR(50) NOT NULL,
    secondname VARCHAR(20),
    lastname VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    salary INT NOT NULL,
    location VARCHAR(20) NOT NULL DEFAULT 'Bangalore'
  );
  ```

- **Giving location NULL**:
  ```sql
  INSERT INTO employee(firstname,secondname,lastname,age,salary, location) 
  VALUES('Jake','Pol','Gupta',28,100000,NULL);
  ```
  Error: `ERROR 1048 (23000): Column 'location' cannot be null`
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
