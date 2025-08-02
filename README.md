# 📈 Sales Prediction Dashboard

A desktop-based Python application that provides a graphical interface for visualizing and analyzing sales data using charts and statistical plots. Built with Tkinter and integrated with a MySQL database, this tool supports user authentication, data exploration, and insightful revenue visualizations.

## 🔧 Features

- 🔐 **User Authentication**
  - Login and signup support with role selection (Analyst, Manager, CEO)

- 📊 **Sales Dashboard**
  - View full sales dataset in a table
  - Generate multiple types of sales analytics graphs:
    - Bar Chart: Revenue by Category
    - Line Chart: Revenue Over Time
    - Pie Chart: Revenue Share by Category
    - Box Plot: Revenue Distribution

- 💾 **Database Integration**
  - Connects to MySQL (`sales_prediction` database)
  - Fetches and inserts data from/to the `sales` and `users` tables

- 🧮 **Data Visualization**
  - Built with `matplotlib` and `seaborn` for advanced charting
  - Interactive multi-page graph viewer with navigation buttons

## 🛠️ Technologies Used

- **Python** — Core application logic
- **Tkinter** — GUI framework
- **MySQL** — Database backend
- **Pandas** — Data handling
- **Matplotlib / Seaborn** — Data visualization

## 🚀 Setup Instructions

### 1. Install Dependencies
    ```bash
    pip install pandas seaborn matplotlib mysql-connector-python

### 2. MySQL Database Setup

    Create Database Sales_Prediction;
    Use Sales_Prediction;
    CREATE TABLE users (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    USERNAME VARCHAR(50) NOT NULL UNIQUE,
    PASSWORD VARCHAR(100) NOT NULL,
    ROLE ENUM('Admin', 'Sales_Manager', 'Analyst') NOT NULL
    );
    INSERT INTO users (USERNAME, PASSWORD, ROLE)
    VALUES 
    ('admin', 'admin123', 'Admin'),
    ('manager', 'manager123', 'Sales_Manager'),
    ('analyst', 'analyst123', 'Analyst');
    
    CREATE TABLE sales (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Product_Name VARCHAR(100) NOT NULL,
    Category VARCHAR(50),
    Sales_Date DATE,
    Quantity_Sold INT,
    Revenue DECIMAL(10,2)
    );
    
    INSERT INTO sales (Product_Name, Category, Sales_Date, Quantity_Sold, Revenue) VALUES ('Smartphone X', 'Electronics', '2025-04-01', 10, 5000.00),
                                                                                          ('LED TV 42"', 'Electronics', '2025-04-03', 5, 3500.00),
                                                                                          ('Shoes - Casual', 'Footwear', '2025-04-05', 20, 1200.00),
                                                                                          ('Laptop Pro', 'Electronics', '2025-04-06', 3, 4500.00),
                                                                                          ('Fitness Tracker', 'Wearable', '2025-04-07', 8, 1600.00),
                                                                                          ('Washing Machine', 'Appliances', '2025-04-08', 2, 7000.00),
                                                                                          ('Microwave Oven', 'Appliances', '2025-04-08', 4, 3600.00),
                                                                                          ('Smartwatch', 'Wearable', '2025-04-09', 7, 2450.00),
                                                                                          ('Headphones', 'Audio', '2025-04-09', 6, 1800.00),
                                                                                          ('Blender', 'Kitchen', '2025-04-10', 5, 1250.00),
                                                                                          ('Shoes - Running', 'Footwear', '2025-04-11', 9, 1900.00),
                                                                                          ('Power Bank', 'Accessories', '2025-04-11', 15, 1500.00),
                                                                                          ('TV 55"', 'Electronics', '2025-04-12', 3, 6000.00),
                                                                                          ('Smartphone Y', 'Electronics', '2025-04-12', 6, 4200.00),
                                                                                          ('Laptop Air', 'Electronics', '2025-04-13', 4, 5200.00),
                                                                                          ('Refrigerator', 'Appliances', '2025-04-13', 2, 9500.00),
                                                                                          ('Iron Box', 'Appliances', '2025-04-14', 10, 3000.00),
                                                                                          ('Speaker Set', 'Audio', '2025-04-14', 3, 2700.00),
                                                                                          ('Mouse', 'Accessories', '2025-04-14', 10, 500.00),
                                                                                          ('Backpack', 'Accessories', '2025-04-15', 12, 1800.00);
                                                                                          
    CREATE TABLE customers (
    Customer_ID INT AUTO_INCREMENT PRIMARY KEY,
    Customer_Name VARCHAR(100) NOT NULL,
    Contact_info VARCHAR(255),
    Purchase_History TEXT
    );
    INSERT INTO customers (Customer_Name, Contact_info, Purchase_History) VALUES 
    ('Ravi Kumar', 'ravi@example.com', 'Smartphone X, LED TV'),
    ('Sneha Mehta', 'sneha@example.com', 'Shoes - Casual'),
    ('Arjun Patel', 'arjun@example.com', 'LED TV'),
    ('Deepa Shah', 'deepa@example.com', 'Laptop Pro'),
    ('Rahul Verma', 'rahul@example.com', 'Fitness Tracker, Earphones'),
    ('Priya Reddy', 'priya@example.com', 'Washing Machine'),
    ('Karan Malhotra', 'karan@example.com', 'Microwave Oven, Blender'),
    ('Aarti Joshi', 'aarti@example.com', 'Laptop Pro'),
    ('Nikhil Yadav', 'nikhil@example.com', 'Smartwatch'),
    ('Divya Jain', 'divya@example.com', 'Headphones, Speaker Set'),
    ('Imran Sheikh', 'imran@example.com', 'Shoes - Running'),
    ('Meena Kapoor', 'meena@example.com', 'Smartphone Y, Power Bank'),
    ('Vikram Sinha', 'vikram@example.com', 'TV 55", Washing Machine'),
    ('Neha Desai', 'neha@example.com', 'Smartphone Z'),
    ('Anil Rao', 'anil@example.com', 'Blender'),
    ('Ritu Garg', 'ritu@example.com', 'Smartwatch'),
    ('Tarun Bansal', 'tarun@example.com', 'Refrigerator, Iron Box'),
    ('Suman Lata', 'suman@example.com', 'LED TV 42"'),
    ('Aman Tripathi', 'aman@example.com', 'Laptop Air, Mouse'),
    ('Kavita Singh', 'kavita@example.com', 'Shoes - Casual, Backpack');


   
