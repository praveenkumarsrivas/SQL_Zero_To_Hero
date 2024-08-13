<h2>Before understanding the concept of Foreign key we will consider the use case first:</h2>

**Let's take a scenario where we have a student table:**

- **student_id**
- **student_fname**
- **student_lname**
- **student_mname**
- **student_email**
- **student_phone**
- **student_alternate_phone**
- **enrollment_date**
- **years_of_exp**
- **student_company**
- **batch_date**
- **source_of_joining**
- **location** `varchar(30)`

### Creating database `cs_portal` and `student` table:
#### Create database `cs_portal`:
```sql
create database cs_portal;
Query OK, 1 row affected (0.02 sec)
```

#### Create table student
```sql
CREATE TABLE student (
    student_id INT AUTO_INCREMENT,
    student_fname VARCHAR(50) NOT NULL,
    student_lname VARCHAR(50) NOT NULL,
    student_mname VARCHAR(50),
    student_email VARCHAR(100) NOT NULL,
    student_phone VARCHAR(15) NOT NULL,
    student_alternate_phone VARCHAR(15),
    enrollment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP NOT NULL,
    years_of_exp INT NOT NULL,
    student_company VARCHAR(100),
    batch_date varchar(30) NOT NULL,
    source_of_joining VARCHAR(30) NOT NULL,
    location VARCHAR(30) NOT NULL,
    primary key (student_id),
    unique key (student_email)
);

desc student;  
+-------------------------+--------------+------+-----+-------------------+-------------------
| Field                   | Type         | Null | Key | Default           | Extra             |
+-------------------------+--------------+------+-----+-------------------+-------------------+
| student_id              | int          | NO   | PRI | NULL              | auto_increment    |
| student_fname           | varchar(50)  | NO   |     | NULL              |                   |
| student_lname           | varchar(50)  | NO   |     | NULL              |                   |
| student_mname           | varchar(50)  | YES  |     | NULL              |                   |
| student_email           | varchar(100) | NO   | UNI | NULL              |                   |
| student_phone           | varchar(15)  | NO   |     | NULL              |                   |
| student_alternate_phone | varchar(15)  | YES  |     | NULL              |                   |
| enrollment_date         | timestamp    | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
| years_of_exp            | int          | NO   |     | NULL              |                   |
| student_company         | varchar(100) | YES  |     | NULL              |                   |
| batch_date              | varchar(30)  | NO   |     | NULL              |                   |
| source_of_joining       | varchar(30)  | NO   |     | NULL              |                   |
| location                | varchar(30)  | NO   |     | NULL              |                   |
+-------------------------+--------------+------+-----+-------------------+-------------------+
```
***Inserting data***
```sql
INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('John', 'Doe', 'P', 'john.doe@example.com', '1234567890', '0987654321', 5, 'Example Corp', '2023-09-01', 'Online', 'New York');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Jane', 'Smith', 'Q', 'jane.smith@example.com', '2345678901', NULL, 3, 'Tech Solutions', '2023-09-01', 'Referral', 'San Francisco');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Emily', 'Jones', 'R', 'emily.jones@example.com', '3456789012', '1234567890', 2, 'Innovatech', '2023-09-01', 'Event', 'Austin');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Michael', 'Brown', 'S', 'michael.brown@example.com', '4567890123', NULL, 6, 'Startup Hub', '2023-09-01', 'Online', 'Seattle');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Chloe', 'Davis', 'T', 'chloe.davis@example.com', '5678901234', '2345678901', 1, NULL, '2023-09-01', 'Online', 'Boston');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('William', 'Wilson', 'U', 'william.wilson@example.com', '6789012345', NULL, 4, 'Enterprise Inc', '2023-09-01', 'Job Fair', 'Chicago');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Emma', 'Martinez', 'V', 'emma.martinez@example.com', '7890123456', '3456789012', 7, 'Global Tech', '2023-09-01', 'Referral', 'Miami');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Ethan', 'Taylor', 'W', 'ethan.taylor@example.com', '8901234567', NULL, 10, 'Digital Arts', '2023-09-01', 'Online', 'San Diego');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Sophia', 'Anderson', 'X', 'sophia.anderson@example.com', '9012345678', '4567890123', 8, 'Creative Works', '2023-09-01', 'Event', 'Las Vegas');

INSERT INTO student (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, years_of_exp, student_company, batch_date, source_of_joining, location) 
VALUES ('Noah', 'Harris', 'Y', 'noah.harris@example.com', '0123456789', NULL, 9, 'Health Solutions', '2023-09-01', 'Online', 'Philadelphia');
```

#### Viewing few columns from the student table
```sql
select student_id, enrollment_date, student_fname, student_email, years_of_exp, student_company, batch_date, source_of_joining, location from student;
+------------+---------------------+---------------+-----------------------------+--------------+------------------+------------+-------------------+---------------+
| student_id | enrollment_date     | student_fname | student_email               | years_of_exp | student_company  | batch_date | source_of_joining | location      |
+------------+---------------------+---------------+-----------------------------+--------------+------------------+------------+-------------------+---------------+
|          1 | 2024-08-13 23:43:51 | John          | john.doe@example.com        |            5 | Example Corp     | 2023-09-01 | Online            | New York      |
|          2 | 2024-08-13 23:43:51 | Jane          | jane.smith@example.com      |            3 | Tech Solutions   | 2023-09-01 | Referral          | San Francisco |
|          3 | 2024-08-13 23:43:51 | Emily         | emily.jones@example.com     |            2 | Innovatech       | 2023-09-01 | Event             | Austin        |
|          4 | 2024-08-13 23:43:51 | Michael       | michael.brown@example.com   |            6 | Startup Hub      | 2023-09-01 | Online            | Seattle       |
|          5 | 2024-08-13 23:43:51 | Chloe         | chloe.davis@example.com     |            1 | NULL             | 2023-09-01 | Online            | Boston        |
|          6 | 2024-08-13 23:43:51 | William       | william.wilson@example.com  |            4 | Enterprise Inc   | 2023-09-01 | Job Fair          | Chicago       |
|          7 | 2024-08-13 23:43:51 | Emma          | emma.martinez@example.com   |            7 | Global Tech      | 2023-09-01 | Referral          | Miami         |
|          8 | 2024-08-13 23:43:51 | Ethan         | ethan.taylor@example.com    |           10 | Digital Arts     | 2023-09-01 | Online            | San Diego     |
|          9 | 2024-08-13 23:43:51 | Sophia        | sophia.anderson@example.com |            8 | Creative Works   | 2023-09-01 | Event             | Las Vegas     |
|         10 | 2024-08-13 23:43:53 | Noah          | noah.harris@example.com     |            9 | Health Solutions | 2023-09-01 | Online            | Philadelphia  |
+------------+---------------------+---------------+-----------------------------+--------------+------------------+------------+-------------------+---------------+
```

### Creating another table `courses`
```sql
create table courses(
  course_id int NOT NULL,
  course_name varchar(30) NOT NULL,
  course_duration_months int NOT NULL,
  course_fee int NOT NULL,
  PRIMARY KEY(course_id)
);
```
- Inserting data to courses table
```sql
insert into courses values(1, 'big data', 6, 50000);
insert into courses values(2, 'web development', 3, 20000);
insert into courses values(3, 'data science', 6, 40000);
insert into courses values(4, 'devops', 1, 10000);

select * from courses;
+-----------+-----------------+------------------------+------------+
| course_id | course_name     | course_duration_months | course_fee |
+-----------+-----------------+------------------------+------------+
|         1 | big data        |                      6 |      50000 |
|         2 | web development |                      3 |      20000 |
|         3 | data science    |                      6 |      40000 |
|         4 | devops          |                      1 |      10000 |
+-----------+-----------------+------------------------+------------+
```

##### Note: If we want to connect the course table with student we need some foreign key that will help in connecting bot the table and form some kind of relationship between them.

**1.To do that we need to add `selected_course` in student table**
  - For this we will drop the student table;
```sql
drop table student;
```
  - Now we will create a students table with `selected_course` column.
```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT,
    student_fname VARCHAR(50) NOT NULL,
    student_lname VARCHAR(50) NOT NULL,
    student_mname VARCHAR(50),
    student_email VARCHAR(100) NOT NULL,
    student_phone VARCHAR(15) NOT NULL,
    student_alternate_phone VARCHAR(15),
    enrollment_date TIMESTAMP NOT NULL,
    years_of_exp INT NOT NULL,
    selected_course INT NOT NULL DEFAULT 1,
    student_company VARCHAR(100),
    batch_date varchar(30) NOT NULL,
    source_of_joining VARCHAR(30) NOT NULL,
    location VARCHAR(30) NOT NULL,
    primary key (student_id),
    unique key (student_email)
);
```

  - Insert data into students table now
```sql
INSERT INTO students 
(student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
VALUES 
('Virat', 'Kohli', NULL, 'virat.kohli@example.com', '9000012345', '9000098765', CURRENT_TIMESTAMP, 10, 1, 'Cricket Academy', '2023-09-20', 'Online', 'Delhi');

INSERT INTO students 
(student_fname, student_lname, student_mname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
VALUES 
('Rohit', 'Sharma', NULL, 'rohit.sharma@example.com', '9100012345', CURRENT_TIMESTAMP, 8, 2, 'Sports Management', '2023-10-05', 'Referral', 'Mumbai');

INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
VALUES 
('Shikhar', 'Dhawan', 'shikhar.dhawan@example.com', '9200123456', CURRENT_TIMESTAMP, 9, 3, '2023-09-15', 'Event', 'Hyderabad');

INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, student_alternate_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
VALUES 
('Ishant', 'Sharma', 'ishant.sharma@example.com', '9300012345', '9300098765', CURRENT_TIMESTAMP, 7, 4, '2023-11-01', 'Online', 'Kolkata');

INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
VALUES 
('Jasprit', 'Bumrah', 'jasprit.bumrah@example.com', '9400012345', CURRENT_TIMESTAMP, 6, 1, '2023-10-20', 'Online', 'Ahmedabad');

INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
VALUES 
('Yuvraj', 'Singh', 'yuvraj.singh@example.com', '9500012345', CURRENT_TIMESTAMP, 12, 2, 'Sports Club', '2023-10-10', 'Referral', 'Chandigarh');

INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
VALUES 
('Ravindra', 'Jadeja', 'ravindra.jadeja@example.com', '9600012345', CURRENT_TIMESTAMP, 11, 3, '2023-09-25', 'Online', 'Rajkot');

INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
VALUES 
('Hardik', 'Pandya', 'hardik.pandya@example.com', '9700012345', CURRENT_TIMESTAMP, 5, 5, 'Fitness Center', '2023-12-01', 'Job Fair', 'Baroda');
```

  - Viewing the data
```sql
select student_id, enrollment_date,selected_course, student_fname, years_of_exp, student_company, batch_date, source_of_joining, location from students;

+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
| student_id | enrollment_date     | selected_course | student_fname | years_of_exp | student_company   | batch_date | source_of_joining | location   |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
|          1 | 2024-08-14 00:12:38 |               1 | Virat         |           10 | Cricket Academy   | 2023-09-20 | Online            | Delhi      |
|          2 | 2024-08-14 00:12:38 |               2 | Rohit         |            8 | Sports Management | 2023-10-05 | Referral          | Mumbai     |
|          3 | 2024-08-14 00:12:38 |               3 | Shikhar       |            9 | NULL              | 2023-09-15 | Event             | Hyderabad  |
|          4 | 2024-08-14 00:12:38 |               4 | Ishant        |            7 | NULL              | 2023-11-01 | Online            | Kolkata    |
|          5 | 2024-08-14 00:12:38 |               1 | Jasprit       |            6 | NULL              | 2023-10-20 | Online            | Ahmedabad  |
|          6 | 2024-08-14 00:12:38 |               2 | Yuvraj        |           12 | Sports Club       | 2023-10-10 | Referral          | Chandigarh |
|          7 | 2024-08-14 00:12:38 |               3 | Ravindra      |           11 | NULL              | 2023-09-25 | Online            | Rajkot     |
|          8 | 2024-08-14 00:12:39 |               5 | Hardik        |            5 | Fitness Center    | 2023-12-01 | Job Fair          | Baroda     |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+

```

#### Importatnt warning:
*We have seen there are only 4 course ids are there (1,2,3,4) but the `Hardik pandya` with `student_id 8 `has choosen the course id 5 which is not even exist in courses table Hence to handle such cases the term `FOREIGN KEY` Introduced.*

### Q: What is foreign key:
***A foreign key is a column or a group of columns in a database table that provides a link between data in two tables. It acts as a cross-reference between tables because it references the primary key of another table, thereby establishing a relationship between them. This ensures the referential integrity of the data, meaning that relationships between tables are consistent and the database enforces the correctness of these relationships.***

  - Now we can say that  `STUDENTS` table dependent on `COURSES` table.
  - we can say that `COURSES` table is the parent table and `STUDENTS` table is the child table.
  
##### Now we need to add `foreign key` in `students` table so that it should not accept the `course_id` which is out of the scope of the `courses` table

  1. Drop the table students
   ```sql
   drop table students;
   ```
  2. create new table with course_id as foreign key
  ```sql
  CREATE TABLE students (
  student_id INT AUTO_INCREMENT,
  student_fname VARCHAR(50) NOT NULL,
  student_lname VARCHAR(50) NOT NULL,
  student_mname VARCHAR(50),
  student_email VARCHAR(100) NOT NULL,
  student_phone VARCHAR(15) NOT NULL,
  student_alternate_phone VARCHAR(15),
  enrollment_date TIMESTAMP NOT NULL,
  years_of_exp INT NOT NULL,
  selected_course INT NOT NULL DEFAULT 1,
  student_company VARCHAR(100),
  batch_date varchar(30) NOT NULL,
  source_of_joining VARCHAR(30) NOT NULL,
  location VARCHAR(30) NOT NULL,
  FOREIGN KEY(selected_course) REFERENCES courses(course_id), <=== we have defined the foreign key
  primary key (student_id),
  unique key (student_email)
    );
  
  ```
```
desc table students:
+-------------------------+--------------+------+-----+---------+----------------+
| Field                   | Type         | Null | Key | Default | Extra          |
+-------------------------+--------------+------+-----+---------+----------------+
| student_id              | int          | NO   | PRI | NULL    | auto_increment |
| student_fname           | varchar(50)  | NO   |     | NULL    |                |
| student_lname           | varchar(50)  | NO   |     | NULL    |                |
| student_mname           | varchar(50)  | YES  |     | NULL    |                |
| student_email           | varchar(100) | NO   | UNI | NULL    |                |
| student_phone           | varchar(15)  | NO   |     | NULL    |                |
| student_alternate_phone | varchar(15)  | YES  |     | NULL    |                |
| enrollment_date         | timestamp    | NO   |     | NULL    |                |
| years_of_exp            | int          | NO   |     | NULL    |                |
| selected_course         | int          | NO   | MUL | 1       |                |
| student_company         | varchar(100) | YES  |     | NULL    |                |
| batch_date              | varchar(30)  | NO   |     | NULL    |                |
| source_of_joining       | varchar(30)  | NO   |     | NULL    |                |
| location                | varchar(30)  | NO   |     | NULL    |                |
+-------------------------+--------------+------+-----+---------+----------------+

```
  3. Inserting data to students
  
  ```sql
  INSERT INTO students 
  (student_fname, student_lname, student_mname, student_email, student_phone, student_alternate_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
  VALUES 
  ('Virat', 'Kohli', NULL, 'virat.kohli@example.com', '9000012345', '9000098765', CURRENT_TIMESTAMP, 10, 1, 'Cricket Academy', '2023-09-20', 'Online', 'Delhi');

  INSERT INTO students 
  (student_fname, student_lname, student_mname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
  VALUES 
  ('Rohit', 'Sharma', NULL, 'rohit.sharma@example.com', '9100012345', CURRENT_TIMESTAMP, 8, 2, 'Sports Management', '2023-10-05', 'Referral', 'Mumbai');

  INSERT INTO students 
  (student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
  VALUES 
  ('Shikhar', 'Dhawan', 'shikhar.dhawan@example.com', '9200123456', CURRENT_TIMESTAMP, 9, 3, '2023-09-15', 'Event', 'Hyderabad');

  INSERT INTO students 
  (student_fname, student_lname, student_email, student_phone, student_alternate_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
  VALUES 
  ('Ishant', 'Sharma', 'ishant.sharma@example.com', '9300012345', '9300098765', CURRENT_TIMESTAMP, 7, 4, '2023-11-01', 'Online', 'Kolkata');

  INSERT INTO students 
  (student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
  VALUES 
  ('Jasprit', 'Bumrah', 'jasprit.bumrah@example.com', '9400012345', CURRENT_TIMESTAMP, 6, 1, '2023-10-20', 'Online', 'Ahmedabad');

  INSERT INTO students 
  (student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
  VALUES 
  ('Yuvraj', 'Singh', 'yuvraj.singh@example.com', '9500012345', CURRENT_TIMESTAMP, 12, 2, 'Sports Club', '2023-10-10', 'Referral', 'Chandigarh');

  INSERT INTO students 
  (student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, batch_date, source_of_joining, location) 
  VALUES 
  ('Ravindra', 'Jadeja', 'ravindra.jadeja@example.com', '9600012345', CURRENT_TIMESTAMP, 11, 3, '2023-09-25', 'Online', 'Rajkot');
  ```
***Now inserting the course_id 5 `hardik pandya` record***
```sql
INSERT INTO students 
(student_fname, student_lname, student_email, student_phone, enrollment_date, years_of_exp, selected_course, student_company, batch_date, source_of_joining, location) 
VALUES 
('Hardik', 'Pandya', 'hardik.pandya@example.com', '9700012345', CURRENT_TIMESTAMP, 5, 5, 'Fitness Center', '2023-12-01', 'Job Fair', 'Baroda');
```
***ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`cs_portal`.`students`, CONSTRAINT `students_ibfk_1` FOREIGN KEY (`selected_course`) REFERENCES `courses` (`course_id`))***


- Viewing the data:
```sql
select student_id, enrollment_date,selected_course, student_fname, years_of_exp, student_company, batch_date, source_of_joining, location from students;

+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
| student_id | enrollment_date     | selected_course | student_fname | years_of_exp | student_company   | batch_date | source_of_joining | location   |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
|          1 | 2024-08-14 00:37:54 |               1 | Virat         |           10 | Cricket Academy   | 2023-09-20 | Online            | Delhi      |
|          2 | 2024-08-14 00:37:54 |               2 | Rohit         |            8 | Sports Management | 2023-10-05 | Referral          | Mumbai     |
|          3 | 2024-08-14 00:37:54 |               3 | Shikhar       |            9 | NULL              | 2023-09-15 | Event             | Hyderabad  |
|          4 | 2024-08-14 00:37:54 |               4 | Ishant        |            7 | NULL              | 2023-11-01 | Online            | Kolkata    |
|          5 | 2024-08-14 00:37:54 |               1 | Jasprit       |            6 | NULL              | 2023-10-20 | Online            | Ahmedabad  |
|          6 | 2024-08-14 00:37:54 |               2 | Yuvraj        |           12 | Sports Club       | 2023-10-10 | Referral          | Chandigarh |
|          7 | 2024-08-14 00:37:58 |               3 | Ravindra      |           11 | NULL              | 2023-09-25 | Online            | Rajkot     |
+------------+---------------------+-----------------+---------------+--------------+-------------------+------------+-------------------+------------+
```

### Scenario:
What if i want to delete the course_id 2 from the courses table, will that allowed?
```sql
delete from courses where course_id=2;
```
ERROR 1451 (23000): Cannot delete or update a parent row: a foreign key constraint fails (`cs_portal`.`students`, CONSTRAINT `students_ibfk_1` FOREIGN KEY (`selected_course`) REFERENCES `courses` (`course_id`))

### Scenario:
what if we update the course_id 2 to 10 in courses table?
```sql
update courses set course_id=10 where course_id=2;
```
ERROR 1451 (23000): Cannot delete or update a parent row: a foreign key constraint fails (`cs_portal`.`students`, CONSTRAINT `students_ibfk_1` FOREIGN KEY (`selected_course`) REFERENCES `courses` (`course_id`))


# what is Database Constraints?
In a database, **constraints** are rules enforced on data columns within a table. They help ensure the accuracy and reliability of the data. Common types of constraints include:

- **Primary Key**: Ensures each row in a table is unique and cannot be null.
- **Foreign Key**: Maintains a valid link between the keys in two different tables, ensuring referential integrity.
- **Unique**: Guarantees that all values in a column are different.
- **Check**: Ensures the value in a column meets a specific condition.
- **Not Null**: Prevents a column from having a null value.
- **Default**: Sets a default value for a column when no value is specified during data entry.

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