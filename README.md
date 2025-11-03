## student_db
Student Database Management System using SQL

This repository hosts a practical SQL project focused on designing, implementing, and querying a simple database for managing college student information, courses, faculty, and enrollments.
The goal was to apply core SQL concepts to analyze student performance, course popularity, and faculty workloads using realistic data.
Technologies Used:

Database Management System: SQLite
Language: SQL (Structured Query Language)

## SQL skills demonstrated
The project's SQL implementation demonstrates foundational and intermediate database skills,
starting with Data Definition Language (DDL) to create a well-structured college management database. 
This includes defining tables like STUDENTS and COURSES and enforcing data integrity with PRIMARY KEY and FOREIGN KEY constraints. 
The use of Data Manipulation Language (DML) is shown through INSERT statements to populate the tables with sample data. Furthermore,
the queries showcase a strong understanding of complex data retrieval using JOIN operations, aggregate functions like COUNT,
and advanced techniques such as CASE statements and subqueries to perform analytical tasks like finding the most popular course or a student's performance
## ER- diagram
<img width="607" height="491" alt="ER-student_db" src="https://github.com/user-attachments/assets/82d09f49-2395-495b-998e-59379b22a600" />

## Database Setup and Query Execution Guide (DBeaver & SQLite)
### Prerequisites
1. DBeaver: Ensure you have DBeaver Community Edition (CE) or Ultimate installed.
2. SQLite Driver: DBeaver typically includes this, but it will prompt you to download it if necessary during the connection setup.

** Step 1.  Download DBeaver and Connect to SQLite Launch DBeaver.
In the top menu, click Database > New Connection.
In the connection wizard, select SQLite from the list of databases and click Next.

** Step 2. Create the Database File
In the connection settings window, under the Main tab, you will see a field labeled Database file.
Click the Browse button.
Navigate to a desired location on your computer (e.g., your project folder), type in a name for your database file (e.g., student-db.sqlite), and click Save.
DBeaver may prompt you to download the necessary SQLite JDBC driver. Click Download if prompted.
Click Finish to establish the connection.


 ** Step 3. Create the Schema and Tables
In the Database Navigator pane on the left, expand your new student-db.sqlite connection.
Right-click on the database name (or the "Schemas" folder/ "main" schema) and select New SQL Editor.
Copy and paste the provided SQL Data Definition Language (DDL) scripts into the editor. This includes all the CREATE TABLE statements.
### Example Snippet of Code to Paste:
CREATE TABLE DEPARTMENTS (
    department_id TEXT PRIMARY KEY,
    department_name TEXT NOT NULL,
    hod_id TEXT 
)

-- ... other CREATE TABLE statements ...

### Execute the schema creation:
* Select all the CREATE TABLE commands in the editor.
* Press the keyboard shortcut Ctrl + Enter (Windows/Linux) or Cmd + Enter (Mac).
* Confirm that the "Output" window shows successful execution with no errors.
  
** Step 4: Insert Data Values
In the same SQL editor (or a new one), copy and paste all the provided INSERT INTO statements.
Example Snippet of Code to Paste:

INSERT INTO DEPARTMENTS VALUES 
('CS', 'Computer Science', 'F001'),
('EC', 'Electronics', 'F003'),
('ME', 'Mechanical', 'F005'),
('CE', 'Civil', 'F007'),
('MA', 'Mathematics', 'F009'),
('PH', 'Physics', 'F010');

### Execute the data insertion:
* Select all the INSERT INTO commands.
* Press Ctrl + Enter (or Cmd + Enter).
*The "Output" window should confirm that multiple rows were inserted successfully.
** Step 5: Write and Execute Queries
* You are now ready to run analysis queries against the populated database.
* Copy and paste the problem-solving queries into your SQL editor (e.g., the queries provided in the previous response).
### To run a specific query:
* Click anywhere inside the single query you wish to execute.
* Press the shortcut Ctrl + Enter (or Cmd + Enter).
* The results will appear in the Results tab at the bottom of the screen.

## Sample queries with output
### 1. Display the courses with students enrollment.
select 
 s.name, 
 c.course_name,
  count(s.name) as student_enrollment
from ENROLLMENTS e  left join STUDENTS s  on s.student_id = e.student_id 
left join COURSES c on c.course_id = e.course_id group by c.course_name;

<img width="483" height="232" alt="op1" src="https://github.com/user-attachments/assets/c645c621-a58e-43d4-b759-987d6e779fb3" />

### 2. Which course has the highest enrollment?
select 
c.course_id,
c.course_name,
count(c.course_id ) 
 from COURSES c left join ENROLLMENTS e on c.course_id = e.course_id 
 group by c.course_id having c.course_id in (
   select e.course_id from ENROLLMENTS e 
   group by e.course_id having count(course_id)= (
     select count(e.course_id)count_of_student_enrollment from ENROLLMENTS e  
     group by e.course_id order by count_of_student_enrollment desc limit 1)); 
<img width="511" height="93" alt="op2" src="https://github.com/user-attachments/assets/f47da142-102b-4d2b-967f-34050653cee8" />



