📄 Student Management System – Project Details
📌 1. Project Description
The Student Management System is a web-based application developed using Core Java, Servlets, JDBC, HTML, and CSS. The purpose of this project is to manage student data efficiently by performing CRUD operations (Create, Read, Update, Delete).
Users can add new student details such as name, email, and course. The system stores this information in a database and allows users to view, update, or delete records as needed. The backend logic is handled by Java Servlets, while JDBC is used to connect and interact with the database. The frontend is designed using HTML and CSS to provide a simple and user-friendly interface.
This project helps in understanding how web applications work using Java technologies and how frontend and backend systems interact with each other.
⭐ 2. Features
➕ Add new student records
📋 View all student details
✏️ Update existing student information
❌ Delete student records
🔗 Database connectivity using JDBC
🌐 Simple and user-friendly interface
💻 3. Technology Used
Programming Language: Java
Backend: Servlet (Java EE / Jakarta EE)
Frontend: HTML, CSS
Database: MySQL
Connectivity: JDBC
Server: Apache Tomcat
🗄️ 4. Database Configuration
Database Setup (MySQL)
SQL
CREATE DATABASE studentdb;

USE studentdb;

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    email VARCHAR(50),
    course VARCHAR(50)
);
JDBC Configuration (in Java)
Java
Connection con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/studentdb",
    "root",
    "password"
);
👉 Make sure:
MySQL is running
Database name = studentdb
Username & password are correct
▶️ 5. How to Run the Project
Install Required Software
Install Java (JDK)
Install MySQL
Install Apache Tomcat Server
Use IDE (Eclipse / NetBeans)
Setup Database
Open MySQL
Run the SQL commands (given above)
Import Project
Open IDE
Import project as Dynamic Web Project
Configure Server
Add Apache Tomcat server in IDE
Deploy project on server
Run Project
Start Tomcat server
Open browser
Run URL:

http://localhost:8080/StudentCRUD/
Test Features
Add student
view list
Delete/update record

Author:-
vivek gajjar
Add student
View list
Delete/update records.
