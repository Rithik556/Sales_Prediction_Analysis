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

    CREATE DATABASE sales_prediction;

    CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    password VARCHAR(50),
    role VARCHAR(20)
    );
    
    CREATE TABLE sales (
    id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(100),
    sales_date DATE,
    quantity_sold INT,
    revenue FLOAT
    );



   
