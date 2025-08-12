---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Intro to Deployment
Deployment: Unit 07 - Lesson 02

- [ ] XAMPP / MAMP
- [ ] mySQL
- [ ] Supabase

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
-->

---
transition: slide-left
---

# Install XAMPP
(or MAMP)

- Install Linux, Apache, PHP, mySQL
  - https://www.apachefriends.org/
- aka LAMP stack
- How does this compare with our MERN stack?

---
transition: slide-left
---

# Create a Database

```sql
-- Create a database
CREATE DATABASE SchoolDB;

-- Show existing databases
SHOW DATABASES;

-- Use a specific database
USE SchoolDB;
```


## Exercises
1. Create a database called CompanyDB.
2. Show all databases and switch to CompanyDB.

---
transition: slide-left
---

# Creating Tables

- see data types https://dev.mysql.com/doc/refman/8.4/en/data-types.html

```sql
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT,
    EnrollmentDate DATE
);
```

## Exercises
1. Create a table called Employees with columns: EmployeeID, Name, Position, Salary, HireDate.
2. Create a table called Departments with columns: DepartmentID, DeptName, and Location.
3. Create a table of your choice with columns of your choice


---
transition: slide-left
---

# Inserting Data

```sql
INSERT INTO Students (FirstName, LastName, Age, EnrollmentDate)
VALUES ('John', 'Doe', 18, '2025-08-01');
```

## Exercises
1. Insert 3 employees into the Employees table.
2. Insert 2 departments into the Departments table.
3. Insert data into your custom table

---
transition: slide-left
---

# Reading Data

```sql
-- Select all columns
SELECT * FROM Students;

-- Select specific columns
SELECT FirstName, Age FROM Students;

-- Add WHERE clause
SELECT * FROM Students WHERE Age > 18;
```

## Exercises
1. Select all employees who earn more than 50000.
2. Display only the department names from the Departments table.
3. Display data from your custom table

---
transition: slide-left
---

# Updating Data

```sql
-- Update student age
UPDATE Students
SET Age = 19
WHERE StudentID = 1;
```

## Exercises
1. Change the salary of an employee with a specific ID.
2. Update the location of a department.
3. Update data from your custom table

---
transition: slide-left
---

# Deleting data

```sql
-- Delete a student
DELETE FROM Students WHERE StudentID = 1;
```

## Exercises
1. Delete an employee based on their name.
2. Remove a department with a specific ID.
3. Delete data from your custom table

---
transition: slide-left
---

# Filtering and Sorting

```sql
-- Get top 3 students older than 18, sorted by age ascending
SELECT * FROM Students
WHERE Age > 18
ORDER BY Age ASC
LIMIT 3;
```

## Exercises
1. List the top 5 highest-paid employees with salary greater than 40000, sorted from highest to lowest salary.
2. Show departments located in 'New York' and order them alphabetically by department name.
3. Filter/Sort data from your custom table


---
layout: image-right
transition: slide-left
image: /assets/db.jpg
backgroundSize: 400px 400px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🐬 [mySQL](https://dev.mysql.com/)
- 🌸 [Intro to mySQL](https://scrimba.com/intro-to-sql-c0aviq0aha)
- 🎬 [mySQL Crash Course](https://www.youtube.com/watch?v=9ylj9NR0Lcg)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)


---
transition: slide-left
---

# Using Joins

```sql
CREATE TABLE Courses (
    CourseID INT AUTO_INCREMENT PRIMARY KEY,
    CourseName VARCHAR(100)
);

CREATE TABLE Enrollments (
    StudentID INT,
    CourseID INT,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

-- INNER JOIN
SELECT Students.FirstName, Courses.CourseName
FROM Enrollments
JOIN Students ON Enrollments.StudentID = Students.StudentID
JOIN Courses ON Enrollments.CourseID = Courses.CourseID;
```

## Exercises
1. Create a table Projects and EmployeeProjects (mapping employees to projects). Use a JOIN to list employee names and their project names.
2. Write a query to list students who are not enrolled in any courses (LEFT JOIN + WHERE NULL).


---
transition: slide-left
---

# Homework

- Work on your "Weather App" assignment due Aug 17 midnight EST
   - can submit before due date if you wish