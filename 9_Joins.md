
# SQL Joins Explained with Examples 🚀

## What are SQL Joins? 🔗

In SQL, **joins** are used to combine rows from two or more tables based on a related column between them. Joins help in fetching data from multiple tables and displaying it as a single result set. There are several types of joins in SQL:

- **INNER JOIN** 🤝
- **LEFT JOIN** 👈
- **RIGHT JOIN** 👉
- **FULL OUTER JOIN** 🌐
- **CROSS JOIN** ➗

Let's dive into each type with examples!

---

## 1. INNER JOIN 🤝

**Definition**: The **INNER JOIN** keyword selects records that have matching values in both tables. If there is no match, the result is not included in the final set.

### Example Tables 📝

- **Table: Students**
  | student_id | student_fname | student_lname |
  |------------|---------------|---------------|
  | 1          | John          | Doe           |
  | 2          | Jane          | Smith         |
  | 3          | Bob           | Brown         |

- **Table: Courses**
  | course_id  | course_name   | student_id |
  |------------|---------------|------------|
  | 101        | Math          | 1          |
  | 102        | Science       | 2          |
  | 103        | History       | 4          |

### SQL Query 💻

```sql
SELECT Students.student_fname, Students.student_lname, Courses.course_name
FROM Students
INNER JOIN Courses
ON Students.student_id = Courses.student_id;
```

### Result Set 🎯

| student_fname | student_lname | course_name |
|---------------|---------------|-------------|
| John          | Doe           | Math        |
| Jane          | Smith         | Science     |

**Explanation**: Only students with IDs 1 and 2 have matching entries in both tables. The student with ID 3 (Bob) is not enrolled in any course, and the course with ID 103 does not match any student.

---

## 2. LEFT JOIN 👈

**Definition**: The **LEFT JOIN** (or **LEFT OUTER JOIN**) keyword returns all records from the left table (Students), and the matched records from the right table (Courses). The result is NULL from the right side if there is no match.

### SQL Query 💻

```sql
SELECT Students.student_fname, Students.student_lname, Courses.course_name
FROM Students
LEFT JOIN Courses
ON Students.student_id = Courses.student_id;
```

### Result Set 🎯

| student_fname | student_lname | course_name |
|---------------|---------------|-------------|
| John          | Doe           | Math        |
| Jane          | Smith         | Science     |
| Bob           | Brown         | NULL        |

**Explanation**: Bob is included in the result even though there is no matching course for him. The `course_name` is `NULL` for Bob.

---

## 3. RIGHT JOIN 👉

**Definition**: The **RIGHT JOIN** (or **RIGHT OUTER JOIN**) keyword returns all records from the right table (Courses), and the matched records from the left table (Students). The result is NULL from the left side if there is no match.

### SQL Query 💻

```sql
SELECT Students.student_fname, Students.student_lname, Courses.course_name
FROM Students
RIGHT JOIN Courses
ON Students.student_id = Courses.student_id;
```

### Result Set 🎯

| student_fname | student_lname | course_name |
|---------------|---------------|-------------|
| John          | Doe           | Math        |
| Jane          | Smith         | Science     |
| NULL          | NULL          | History     |

**Explanation**: The course "History" is included in the result even though there is no matching student. The student details are `NULL` for this course.

---

## 4. FULL OUTER JOIN 🌐

**Definition**: The **FULL OUTER JOIN** keyword returns all records when there is a match in either left (Students) or right (Courses) table records. If there is no match, the result is NULL on the side where there is no match.

### SQL Query 💻

```sql
SELECT Students.student_fname, Students.student_lname, Courses.course_name
FROM Students
FULL OUTER JOIN Courses
ON Students.student_id = Courses.student_id;
```

### Result Set 🎯

| student_fname | student_lname | course_name |
|---------------|---------------|-------------|
| John          | Doe           | Math        |
| Jane          | Smith         | Science     |
| Bob           | Brown         | NULL        |
| NULL          | NULL          | History     |

**Explanation**: The result includes all students and courses, whether they have matches or not.

---

## 5. CROSS JOIN ➗

**Definition**: The **CROSS JOIN** keyword returns the Cartesian product of the two tables. This means it returns all possible combinations of rows from both tables.

### SQL Query 💻

```sql
SELECT Students.student_fname, Students.student_lname, Courses.course_name
FROM Students
CROSS JOIN Courses;
```

### Result Set 🎯

| student_fname | student_lname | course_name |
|---------------|---------------|-------------|
| John          | Doe           | Math        |
| John          | Doe           | Science     |
| John          | Doe           | History     |
| Jane          | Smith         | Math        |
| Jane          | Smith         | Science     |
| Jane          | Smith         | History     |
| Bob           | Brown         | Math        |
| Bob           | Brown         | Science     |
| Bob           | Brown         | History     |

**Explanation**: All possible combinations of students and courses are returned.

---

## Summary 🎓

- **INNER JOIN** 🤝: Only returns matching rows.
- **LEFT JOIN** 👈: Returns all rows from the left table, and matched rows from the right table.
- **RIGHT JOIN** 👉: Returns all rows from the right table, and matched rows from the left table.
- **FULL OUTER JOIN** 🌐: Returns all rows when there is a match in either table.
- **CROSS JOIN** ➗: Returns the Cartesian product of the two tables.

---

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
