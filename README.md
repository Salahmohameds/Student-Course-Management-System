# Student Course Management Database Project

## Introduction
This project involves creating and managing a database for student course enrollments. It includes tables for Students, Instructors, Courses, and Enrollments. The project also includes various SQL queries for retrieving, manipulating, and analyzing data.

## Prerequisites

### Installing Microsoft SQL Server and SQL Server Management Studio (SSMS)

1. **Download Microsoft SQL Server:**
   - Visit the [Microsoft SQL Server Downloads page](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
   - Choose the edition you prefer (Developer edition is recommended for development purposes) and download it.

2. **Install SQL Server:**
   - Run the installer and follow the on-screen instructions.
   - During the setup, select the required features, including the Database Engine Services.
   - Configure the server as per your requirements.

3. **Download and Install SQL Server Management Studio (SSMS):**
   - Visit the [SSMS download page](https://aka.ms/ssmsfullsetup) to download the latest version.
   - Run the installer and follow the instructions to complete the installation.

## Database Schema

### Students Table
Contains student details, including an auto-incremented primary key.
```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY IDENTITY(1,1),
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    date_of_birth DATE
);
```

### Instructors Table
Stores instructor information with a primary key.
```sql
CREATE TABLE Instructors (
    instructor_id INT PRIMARY KEY IDENTITY(1,1),
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);
```

### Courses Table
Includes course details and a foreign key referencing the instructor.
```sql
CREATE TABLE Courses (
    course_id INT PRIMARY KEY IDENTITY(1,1),
    course_name VARCHAR(100),
    course_description TEXT,
    instructor_id INT,
    FOREIGN KEY (instructor_id) REFERENCES Instructors(instructor_id)
);
```

### Enrollments Table
Manages the relationship between students and courses with foreign keys referencing both.
```sql
CREATE TABLE Enrollments (
    enrollment_id INT PRIMARY KEY IDENTITY(1,1),
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);
```

## Sample Data

### Insert Statements
Sample data entries for testing the database.

#### Insert Data into Students Table
```sql
INSERT INTO Students (first_name, last_name, email, date_of_birth) VALUES
('Ahmed', 'El-Sayed', 'ahmed.elsayed@gmail.com', '2000-01-15'),
('Mona', 'Hassan', 'mona.hassan@gmail.com', '1999-02-20'),
('Mohamed', 'Ali', 'mohamed.ali@gmail.com', '2001-03-10'),
('Sara', 'Fathy', 'sara.fathy@gmail.com', '1998-04-25'),
('Omar', 'Khaled', 'omar.khaled@gmail.com', '2000-05-30'),
('Laila', 'Nabil', 'laila.nabil@gmail.com', '1999-06-15'),
('Hassan', 'Gamal', 'hassan.gamal@gmail.com', '2001-07-20'),
('Dina', 'Youssef', 'dina.youssef@gmail.com', '1998-08-05'),
('Tamer', 'Khalil', 'tamer.khalil@gmail.com', '1999-09-25'),
('Nadia', 'Farouk', 'nadia.farouk@gmail.com', '2000-10-10'),
('Yasser', 'Adel', 'yasser.adel@gmail.com', '2001-11-15'),
('Fatma', 'Saleh', 'fatma.saleh@gmail.com', '1998-12-05'),
('Khaled', 'Mohsen', 'khaled.mohsen@gmail.com', '2002-03-15');
```

#### Insert Data into Instructors Table
```sql
INSERT INTO Instructors (first_name, last_name, email) VALUES
('Hesham', 'Mansour', 'hesham.mansour@gmail.com'),
('Amina', 'Zaki', 'amina.zaki@gmail.com'),
('Karim', 'Mostafa', 'karim.mostafa@gmail.com'),
('Rania', 'Adel', 'rania.adel@gmail.com'),
('Tarek', 'Nassar', 'tarek.nassar@gmail.com');
```

#### Insert Data into Courses Table
```sql
INSERT INTO Courses (course_name, course_description, instructor_id) VALUES
('Introduction to Programming', 'Basic concepts of programming using Python.', 1),     -- Hesham Mansour
('Data Structures', 'Understanding and implementing various data structures.', 2),    -- Amina Zaki
('Database Systems', 'Introduction to database design and SQL.', 3),                  -- Karim Mostafa
('Computer Networks', 'Fundamentals of computer networking and protocols.', 4),       -- Rania Adel
('Operating Systems', 'Concepts of operating systems and process management.', 5),    -- Tarek Nassar
('Advanced Algorithms', 'In-depth study of advanced algorithmic techniques.', 3);     -- Karim Mostafa
```

#### Insert Data into Enrollments Table
```sql
INSERT INTO Enrollments (student_id, course_id, enrollment_date) VALUES
(1, 1, '2024-01-10'),  
(2, 2, '2024-01-12'),  
(3, 3, '2024-01-14'), 
(4, 4, '2024-01-16'),  
(5, 5, '2024-01-18'), 
(6, 1, '2024-01-20'),  
(7, 2, '2024-01-22'), 
(8, 3, '2024-01-24'), 
(9, 4, '2024-01-26'),  
(10, 5, '2024-01-28'), 
(11, 1, '2024-01-30'), 
(12, 2, '2024-02-01'), 
(1, 3, '2024-02-03'), 
(2, 4, '2024-02-05'),  
(3, 5, '2024-02-07'), 
(4, 1, '2024-02-10'),  
(5, 2, '2024-02-12'),  
(6, 3, '2024-02-14'), 
(7, 4, '2024-02-16'),  
(8, 5, '2024-02-18'),  
(9, 1, '2024-02-20'),  
(10, 2, '2024-02-22'), 
(11, 3, '2024-02-24'),
(12, 4, '2024-02-26');
```

## Basic Queries

### Select All Students
```sql
SELECT * FROM Students;
```
**Output:** This query returns all records from the Students table.

### Select All Courses
```sql
SELECT * FROM Courses;
```
**Output:** This query returns all records from the Courses table.

## Advanced Queries

### Students in a Specific Course
This query retrieves students enrolled in a course named 'Database Systems'.
```sql
SELECT S.first_name, S.last_name, C.course_name
FROM Enrollments E
JOIN Students S ON E.student_id = S.student_id
JOIN Courses C ON E.course_id = C.course_id
WHERE C.course_name = 'Database Systems';
```

### Courses with More Than 5 Students
Identifies courses with high enrollment.
```sql
SELECT C.course_name, COUNT(E.student_id) AS student_count
FROM Enrollments E
JOIN Courses C ON E.course_id = C.course_id
GROUP BY C.course_name
HAVING COUNT(E.student_id) > 5;
```

## Join Queries

### Students and Their Courses
Displays all students along with their enrolled courses.
```sql
SELECT S.first_name, S.last_name, C.course_name
FROM Students S
LEFT JOIN Enrollments E ON S.student_id = E.student_id
LEFT JOIN Courses C ON E.course_id = C.course_id;
```

### Instructors and Their Courses
Lists instructors and the courses they teach.
```sql
SELECT I.first_name, I.last_name, C.course_name
FROM Instructors I
LEFT JOIN Courses C ON I.instructor_id = C.instructor_id;
```

## Subqueries and Set Operations

### Students Enrolled in More Than One Course
Finds students who have taken multiple courses.
```sql
SELECT S.first_name, S.last_name
FROM Students S
WHERE S.student_id IN (
    SELECT E.student_id
    FROM Enrollments E
    GROUP BY E.student_id
    HAVING COUNT(E.course_id) > 1
);
```

### Top 3 Students with Most Enrollments
Identifies the most active students.
```sql
SELECT TOP 3 S.first_name, S.last_name, COUNT(E.enrollment_id) AS enrollment_count
FROM Students S
JOIN Enrollments E ON S.student_id = E.student_id
GROUP

 BY S.first_name, S.last_name
ORDER BY COUNT(E.enrollment_id) DESC;
```

## Functions and Stored Procedures

### Add Student Stored Procedure
Facilitates adding a new student to the database.
```sql
CREATE PROCEDURE AddStudent
    @first_name VARCHAR(50),
    @last_name VARCHAR(50),
    @email VARCHAR(100),
    @date_of_birth DATE
AS
BEGIN
    INSERT INTO Students (first_name, last_name, email, date_of_birth)
    VALUES (@first_name, @last_name, @email, @date_of_birth);
END;
```

### Calculate Age Function
Calculates the age of students from their date of birth.
```sql
CREATE FUNCTION CalculateAge (@date_of_birth DATE)
RETURNS INT
AS
BEGIN
    RETURN DATEDIFF(YEAR, @date_of_birth, GETDATE());
END;
```

## Aggregate Functions and Grouping

### Total Number of Students
Retrieves the total student count.
```sql
SELECT COUNT(*) AS total_students FROM Students;
```

### Average, Minimum, and Maximum Enrollments per Course
Uses aggregate functions to provide enrollment statistics.
```sql
SELECT AVG(student_count) AS average_enrollments, MIN(student_count) AS min_enrollments, MAX(student_count) AS max_enrollments
FROM (
    SELECT course_id, COUNT(student_id) AS student_count
    FROM Enrollments
    GROUP BY course_id
) AS enrollments_per_course;
```

## Additional Tasks

### Aliases for Column Names
Provides user-friendly column names in the result set.
```sql
SELECT S.first_name AS 'Student First Name', S.last_name AS 'Student Last Name', C.course_name AS 'Course Name'
FROM Students S
JOIN Enrollments E ON S.student_id = E.student_id
JOIN Courses C ON E.course_id = C.course_id;
```

### Categorize Students by Age
Categorizes students based on their age.
```sql
SELECT first_name, last_name,
       CASE 
           WHEN DATEDIFF(YEAR, date_of_birth, GETDATE()) < 20 THEN 'Teenager'
           WHEN DATEDIFF(YEAR, date_of_birth, GETDATE()) BETWEEN 20 AND 25 THEN 'Young Adult'
           ELSE 'Adult'
       END AS age_group
FROM Students;
```

## Conclusion

This project provides a comprehensive approach to managing and analyzing student and course data using SQL. With the database schema, sample data, and a variety of queries, you can efficiently handle tasks related to student enrollments, course management, and reporting. 

The provided SQL scripts cover basic to advanced queries, join operations, subqueries, and stored procedures, demonstrating a wide range of SQL capabilities. By utilizing these scripts, you can perform detailed analysis and gain insights into student performance, course popularity, and overall enrollment trends.

Feel free to expand upon this project by adding more features, integrating with other systems, or customizing the queries to fit specific needs. Happy querying!

## Contributions

If you have any suggestions for improvements or new features, please feel free to contribute by submitting a pull request or opening an issue. Your feedback is highly appreciated!

## License

This project is licensed under the [MIT License](LICENSE). See the LICENSE file for more details.



Thank you for checking out this project!

