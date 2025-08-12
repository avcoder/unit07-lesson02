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

# 3rd Normal Form

- Normalization is the process of organizing data in a database to:
  - Eliminate redundancy
  - Ensure data dependencies make sense
  - Improve data integrity
- Normalization is done in stages called normal forms.

---
transition: slide-left
---

# Example Issues

| OrderID | CustomerName | CustomerAddress | ProductName | ProductPrice |
| ------- | ------------ | --------------- | ----------- | ------------ |
| 1001    | Alice Smith  | 123 Main St     | Pen         | 1.50         |
| 1002    | Bob Jones    | 456 Oak Ave     | Notebook    | 2.75         |
| 1003    | Alice Smith  | 123 Main St     | Pencil      | 0.50         |

- CustomerName → CustomerAddress
  - This is a transitive dependency. The CustomerAddress depends on CustomerName, not directly on OrderID.
- ProductName → ProductPrice
  - Another transitive dependency. The price is a property of the product, not the order.
- Redundancy:
  - Alice Smith and her address are repeated in two rows.
  - If the address changes, you have to update it in multiple places (update anomaly).
  - Similarly, if ProductPrice changes, you’d have to find and update every instance.


---
transition: slide-left
---

# Example Solution

| Problem Before                       | After 3NF Fix               |
| ------------------------------------ | --------------------------- |
| Repeated customer info               | Stored once in `Customers`  |
| Product prices stored multiple times | Stored once in `Products`   |
| Risk of inconsistent updates         | Changes update only one row |
| Transitive dependencies              | All removed                 |


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

# Aggregation Functions and Grouping
Use COUNT(), SUM(), AVG(), GROUP BY

```sql
-- Count students by age
SELECT Age, COUNT(*) AS Total
FROM Students
GROUP BY Age;
```

## Exercises
1. Show total number of employees in each department.
2. Find the average salary of employees per department.
3. Try using either COUNT, SUM, AVG, or GROUP BY on your custom table

---
transition: slide-left
---

# Table Constraints

```sql
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100) NOT NULL UNIQUE,
    Duration INT CHECK (Duration > 0)
);
```

1. Create a table Products with a price that must be greater than 0.
2. Add a UNIQUE constraint to the Email column of a Customers table.

---
transition: slide-left
---

# Altering Tables

```sql
-- Add a new column
ALTER TABLE Students ADD COLUMN Email VARCHAR(100);

-- Modify column data type
ALTER TABLE Students MODIFY COLUMN Age TINYINT;

-- Drop a column
ALTER TABLE Students DROP COLUMN Email;
```

1. Add a PhoneNumber column to the Employees table.
2. Change the data type of Salary in Employees from INT to DECIMAL.

---
transition: slide-left
---

# Exercise

- Create a mini database for a Library with:
  - Books table
  - Patrons table
  - Checkout table (who borrowed which book and when)

## Then Try: 
- Inserting sample data
- Writing queries using SELECT, JOIN, WHERE, and GROUP BY
- Performing updates and deletions


---
transition: slide-left
---

# Homework

- Work on your "Weather App" assignment due Aug 17 midnight EST
   - can submit before due date if you wish