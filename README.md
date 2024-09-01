# Student Course Management Database Project

## Introduction
This project is designed to manage student course enrollments in a university setting. The database includes tables for Students, Instructors, Courses, and Enrollments. We also explore various SQL queries to retrieve, manipulate, and analyze data from these tables.

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

### Tables Created

## Students Table
```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY IDENTITY(1,1),
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    date_of_birth DATE
);
```
## Instructors Table

```sql
CREATE TABLE Instructors (
    instructor_id INT PRIMARY KEY IDENTITY(1,1),
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);
```

