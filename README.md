# Java JDBC CRUD with SQL Server

## 🌐 Overview
This is a Java project that demonstrates how to connect to a SQL Server database using JDBC. The project follows the **DAO (Data Access Object)** pattern for better organization, maintainability, and separation of concerns. It includes basic CRUD operations for `Department` and `Seller` entities.

## 🚀 Technologies
* **Java** (8 or higher)
* **JDBC** (Java Database Connectivity)
* **SQL Server**

## ⚙️ Features
- Database connection handling with JDBC.
- DAO pattern implementation for separation of concerns.
- Full CRUD (Create, Read, Update, Delete) operations for `Department` and `Seller` entities.
- Custom exceptions for handling database and integrity errors.

## 📂 Project Structure
```plaintext
/
├── .idea/              # IntelliJ IDEA project settings
├── out/                # Compiled output files
├── src/                # Source code
│   ├── application/    # Entry point classes
│   │   └── Program     # Main program for testing DAO operations
│   ├── db/             # Database utility classes
│   │   ├── DB          # Handles database connections
│   │   ├── DbException # Custom exception for database errors
│   │   └── DbIntegrityException # Custom exception for integrity errors
│   ├── model/          # Core business logic
│   │   ├── dao/        # DAO interfaces and implementations
│   │   │   ├── impl/   # DAO implementations using JDBC
│   │   │   │   ├── DepartmentDaoJDBC
│   │   │   │   └── SellerDaoJDBC
│   │   │   ├── DaoFactory
│   │   │   ├── DepartmentDao
│   │   │   └── SellerDao
│   │   └── entities/   # Entity classes
│   │       ├── Department
│   │       └── Seller
├── .gitignore          # Git ignore file
├── db.properties       # Database connection configuration file
```

## 🧩 DAO Pattern Implementation
* **Interfaces:** `DepartmentDao` and `SellerDao` define the contract for CRUD operations.
* **Implementations:** `DepartmentDaoJDBC` and `SellerDaoJDBC` provide the actual JDBC logic to interact with the database.
* **Factory:** `DaoFactory` provides instances of the DAO implementations, keeping the entry point decoupled from the specific implementation.

## 🛠️ Setup & Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/Lorenzo-Zagallo/java-jdbc-crud.git
   ```
2. Open the project in IntelliJ IDEA (or your preferred Java IDE).
3. Set up the database connection in the `db.properties` file located in the project root:
   ```properties
   db.url=jdbc:sqlserver://localhost:1433;databaseName=cursojdbc
   db.user=yourUsername
   db.password=yourPassword
   ```
4. Make sure your SQL Server is running and execute the script below to create the database and tables.
5. Run the `Program` class in the `application` package to test the operations in the console.

## 🗄️ Database Script

Run this script in your SQL Server Management Studio to set up the required environment:

```sql
CREATE DATABASE cursojdbc;
GO

USE cursojdbc;
GO

CREATE TABLE department (
    id INT PRIMARY KEY IDENTITY(1,1),
    name NVARCHAR(60)
);

CREATE TABLE seller (
    id INT PRIMARY KEY IDENTITY(1,1),
    name NVARCHAR(60) NOT NULL,
    email NVARCHAR(100) NOT NULL,
    birthDate DATETIME NOT NULL,
    baseSalary DECIMAL(10, 2) NOT NULL,
    departmentId INT NOT NULL,
    FOREIGN KEY (departmentId) REFERENCES department(id)
);

INSERT INTO department (name) VALUES 
    ('Computers'),
    ('Electronics'),
    ('Fashion'),
    ('Books');

INSERT INTO seller (name, email, birthDate, baseSalary, departmentId) VALUES 
    ('Bob Brown', 'bob@gmail.com', '1998-04-21 00:00:00', 1000.00, 1),
    ('Maria Green', 'maria@gmail.com', '1979-12-31 00:00:00', 3500.00, 2),
    ('Alex Grey', 'alex@gmail.com', '1988-01-15 00:00:00', 2200.00, 1),
    ('Martha Red', 'martha@gmail.com', '1993-11-30 00:00:00', 3000.00, 4),
    ('Donald Blue', 'donald@gmail.com', '2000-01-09 00:00:00', 4000.00, 3),
    ('Alex Pink', 'bob@gmail.com', '1997-03-04 00:00:00', 3000.00, 2);
```

---

## 👨‍💻 Author

**Lorenzo Zagallo**
* GitHub: [@Lorenzo-Zagallo](https://github.com/Lorenzo-Zagallo)
* LinkedIn: [Lorenzo Zagallo](https://www.linkedin.com/in/lorenzo-zagallo-07654a2b9/)

If you have any questions or suggestions, feel free to open an [issue](https://github.com/Lorenzo-Zagallo/java-jdbc-crud/issues).
