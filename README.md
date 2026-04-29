
🎓 Student CRUD Web Project (Java Servlet + JDBC)
🔧 Technologies Used
Core Java
Servlet (Jakarta / Java EE)
JDBC (Database connectivity)
HTML + CSS (UI)
MySQL Database
📁 Project Structure

StudentCRUD/
│── index.html
│── addStudent.html
│── style.css
│
├── src/
│   ├── AddStudentServlet.java
│   ├── ViewStudentServlet.java
│   ├── UpdateStudentServlet.java
│   ├── DeleteStudentServlet.java
│   ├── DBConnection.java
│
├── WEB-INF/
│   ├── web.xml
🗄️ Database (MySQL)
SQL
CREATE DATABASE studentdb;

USE studentdb;

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    email VARCHAR(50),
    course VARCHAR(50)
);
🔌 DBConnection.java
Java
import java.sql.*;

public class DBConnection {
    public static Connection getConn() {
        Connection con = null;
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/studentdb",
                "root",
                "password"
            );
        } catch(Exception e) {
            System.out.println(e);
        }
        return con;
    }
}
➕ AddStudentServlet.java
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class AddStudentServlet extends HttpServlet {
    protected void doPost(HttpServletRequest req, HttpServletResponse res)
    throws ServletException, IOException {

        String name = req.getParameter("name");
        String email = req.getParameter("email");
        String course = req.getParameter("course");

        try {
            Connection con = DBConnection.getConn();
            PreparedStatement ps = con.prepareStatement(
                "INSERT INTO students(name,email,course) VALUES(?,?,?)"
            );
            ps.setString(1, name);
            ps.setString(2, email);
            ps.setString(3, course);

            ps.executeUpdate();
            res.sendRedirect("view");
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
📖 ViewStudentServlet.java
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class ViewStudentServlet extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse res)
    throws ServletException, IOException {

        PrintWriter out = res.getWriter();
        out.println("<h2>Student List</h2>");

        try {
            Connection con = DBConnection.getConn();
            Statement st = con.createStatement();
            ResultSet rs = st.executeQuery("SELECT * FROM students");

            while(rs.next()) {
                out.println(rs.getInt(1) + " " +
                            rs.getString(2) + " " +
                            rs.getString(3) + " " +
                            rs.getString(4) +
                            " <a href='delete?id="+rs.getInt(1)+"'>Delete</a>");
                out.println("<br>");
            }
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
❌ DeleteStudentServlet.java
Java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class DeleteStudentServlet extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse res)
    throws IOException {

        int id = Integer.parseInt(req.getParameter("id"));

        try {
            Connection con = DBConnection.getConn();
            PreparedStatement ps = con.prepareStatement(
                "DELETE FROM students WHERE id=?"
            );
            ps.setInt(1, id);
            ps.executeUpdate();

            res.sendRedirect("view");
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
📝 index.html (Home Page)
HTML
<html>
<head>
<link rel="stylesheet" href="style.css">
</head>
<body>
<h1>Student Management System</h1>

<a href="addStudent.html">Add Student</a><br><br>
<a href="view">View Students</a>

</body>
</html>
➕ addStudent.html
HTML
<html>
<head>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Add Student</h2>

<form action="add" method="post">
Name: <input type="text" name="name"><br>
Email: <input type="email" name="email"><br>
Course: <input type="text" name="course"><br><br>

<input type="submit" value="Add">
</form>

</body>
</html>
🎨 style.css
CSS
body {
    font-family: Arial;
    text-align: center;
    background: #f2f2f2;
}

h1 {
    color: #333;
}

input {
    margin: 5px;
    padding: 8px;
}
⚙️ web.xml
XML
<web-app>

<servlet>
    <servlet-name>Add</servlet-name>
    <servlet-class>AddStudentServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Add</servlet-name>
    <url-pattern>/add</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>View</servlet-name>
    <servlet-class>ViewStudentServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>View</servlet-name>
    <url-pattern>/view</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>Delete</servlet-name>
    <servlet-class>DeleteStudentServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Delete</servlet-name>
    <url-pattern>/delete</url-pattern>
</servlet-mapping>

</web-app>
🖥️ Output (What You Show in Viva)
You should take screenshots of:
🏠 Home Page
➕ Add Student Form
📋 Student List
❌ Delete Operation
👉 For “animation screenshot”:
Record screen while adding & deleting student
Or take multiple step screenshots
🚀 Bonus (If Teacher Asks)
Add:
Update feature (Edit button)
Bootstrap UI
Search student

Author:-
vivek gajjar
