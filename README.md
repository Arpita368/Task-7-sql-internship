# 📄 Task 7: Creating Views

## 🎯 Objective
Learn to create and use SQL views for simplifying queries, providing abstraction, and improving data security.

## 🛠 Tools
- MySQL Workbench

## 📌 Steps

1️⃣ Create Tables
-----------------
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(30),
    phone VARCHAR(10),
    city VARCHAR(20),
    age INT
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product VARCHAR(20),
    price FLOAT,
    FOREIGN KEY(customer_id) REFERENCES Customers(customer_id)
);

2️⃣ Insert Sample Data
----------------------
INSERT INTO Customers VALUES
(1, 'Ravi Sharma','9745834678', 'Mumbai', 21),
(2, 'Priya Verma','8345587878', 'Delhi', 32),
(3, 'Amit Kumar','9793258778', 'Pune', 25),
(4, 'Neha Singh','9432885346', 'Chennai', 40);

INSERT INTO Orders VALUES
(101, 1, 'Laptop', 55000.00),
(102, 1, 'Keyboard', 1500.00),
(103, 2, 'Smartphone', 18000.00),
(104, 3, 'Tablet', 12000.00);

3️⃣ Creating Views
------------------
-- 🗂 Simple View: Customer names with orders & prices
CREATE VIEW CustomerOrders AS
SELECT C.customer_id, C.name, C.city, O.product, O.price
FROM Customers C
INNER JOIN Orders O ON C.customer_id = O.customer_id;

-- 💰 Filtered View: Orders above 20000
CREATE VIEW HighValueOrders AS
SELECT C.name, O.product, O.price
FROM Customers C
INNER JOIN Orders O ON C.customer_id = O.customer_id
WHERE O.price > 20000;

-- 📊 Aggregated View: Total spending per customer
CREATE VIEW TotalSpending AS
SELECT C.customer_id, C.name, SUM(O.price) AS total_spent
FROM Customers C
INNER JOIN Orders O ON C.customer_id = O.customer_id
GROUP BY C.customer_id, C.name;

4️⃣ Using Views
---------------
SELECT * FROM CustomerOrders;
SELECT * FROM HighValueOrders;
SELECT * FROM TotalSpending;

5️⃣ Dropping a View
-------------------
DROP VIEW IF EXISTS TotalSpending;

## ✅ Outcome
- Simplified complex queries into reusable views
- Applied filtering and aggregation in views
- Increased abstraction and security for database access

## Author
Created by Arpita Jitendra Sonparote
