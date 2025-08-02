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


   ### 3. Python Code

    import tkinter as tk
    from tkinter import messagebox, filedialog, ttk
    import mysql.connector
    import pandas as pd
    import seaborn as sb
    import matplotlib.pyplot as plt
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg

# --- Add Sales Record (Optional Utility Function) ---
    def add_sales_record(product_name, category, quantity, revenue):
    try:
        conn = mysql.connector.connect(host='localhost', user='root', password='1234', database='sales_prediction')
        cursor = conn.cursor()
        query = """
            INSERT INTO sales (product_name, category, sales_date, quantity_sold, revenue)
            VALUES (%s, %s, CURDATE(), %s, %s)
        """
        cursor.execute(query, (product_name, category, quantity, revenue))
        conn.commit()
        conn.close()
    except mysql.connector.Error as err:
        print("Error:", err)


# --- Graph Viewer Function ---
    def generate_graph():
       graph_window = tk.Toplevel()
       graph_window.title("Graph Viewer")
       graph_window.geometry("1000x700")

    canvas = [None]
    page = [0]

    def draw_page(index):
        if canvas[0]:
            canvas[0].get_tk_widget().destroy()

        fig, ax = plt.subplots(figsize=(10, 6))

        conn = mysql.connector.connect(host='localhost', user='root', password='1234', database='sales_prediction')
        df = pd.read_sql("SELECT * FROM sales", conn)
        conn.close()

        if index == 0:
            grouped = df.groupby('Category', as_index=False)['Revenue'].sum().sort_values(by='Revenue', ascending=False)
            sb.barplot(data=grouped, x='Category', y='Revenue', ax=ax, palette='Set2')
            for i, row in grouped.iterrows():
                ax.text(i, row['Revenue'] + row['Revenue'] * 0.01, f"${row['Revenue']:.0f}", ha='center', va='bottom')
            ax.set_title("Bar Plot: Revenue by Category", fontsize=16, pad=20)
            ax.set_xlabel("Category")
            ax.set_ylabel("Revenue ($)")
            ax.tick_params(axis='x', rotation=30)
            ax.grid(axis='y', linestyle='--', alpha=0.6)

        elif index == 1:
            df['Sales_Date'] = pd.to_datetime(df['Sales_Date'])
            date_revenue = df.groupby('Sales_Date').sum().reset_index()
            ax.plot(date_revenue['Sales_Date'], date_revenue['Revenue'], marker='o')
            ax.set_title("Line Plot: Revenue Over Time", fontsize=16, pad=20)
            ax.set_xlabel("Date")
            ax.set_ylabel("Revenue")
            ax.grid(True)

        elif index == 2:
            category_sum = df.groupby('Category')['Revenue'].sum()
            ax.pie(category_sum, labels=category_sum.index, autopct='%1.1f%%', startangle=90)
            ax.set_title("Pie Chart: Revenue Share by Category", fontsize=16, pad=20)

        elif index == 3:
            sorted_cats = df.groupby("Category")["Revenue"].median().sort_values().index
            df['Category'] = pd.Categorical(df['Category'], categories=sorted_cats, ordered=True)
            sb.boxplot(data=df, x='Category', y='Revenue', ax=ax, palette='pastel', width=0.6, showfliers=True)
            sb.stripplot(data=df, x='Category', y='Revenue', ax=ax, color='black', size=3, jitter=0.2)
            ax.set_title("Box Plot: Revenue Distribution by Category", fontsize=16, pad=20)
            ax.set_xlabel("Product Category")
            ax.set_ylabel("Revenue ($)")
            ax.tick_params(axis='x', rotation=30)
            ax.grid(axis='y', linestyle='--', alpha=0.7)

        canvas[0] = FigureCanvasTkAgg(fig, master=graph_window)
        canvas[0].draw()
        canvas[0].get_tk_widget().pack()

    def next_page():
        if page[0] < 3:
            page[0] += 1
            draw_page(page[0])

    def prev_page():
        if page[0] > 0:
            page[0] -= 1
            draw_page(page[0])

    nav_frame = tk.Frame(graph_window)
    nav_frame.pack(pady=10)

    prev_btn = tk.Button(nav_frame, text="← Previous", command=prev_page, font="Terminal")
    next_btn = tk.Button(nav_frame, text="Next →", command=next_page, font="Terminal")

    prev_btn.grid(row=0, column=0, padx=10)
    next_btn.grid(row=0, column=1, padx=10)

    draw_page(page[0])


# --- Open Dashboard After Login ---
    def open_dashboard():
        dashboard = tk.Toplevel(root)
        dashboard.title("Dashboard")
        dashboard.state("zoomed")

    db_frame = tk.Frame(dashboard, padx=20, pady=20)
    db_frame.place(relx=0.5, rely=0.4, anchor="center")

    def view_data():
        try:
            conn = mysql.connector.connect(host='localhost', user='root', password='1234', database='sales_prediction')
            query = "SELECT * FROM sales"
            df = pd.read_sql(query, conn)
            conn.close()

            data_window = tk.Toplevel(dashboard)
            data_window.title("Sales Data")

            tree = ttk.Treeview(data_window)
            tree["columns"] = list(df.columns)
            tree["show"] = "headings"

            for col in df.columns:
                tree.heading(col, text=col)
                tree.column(col, anchor="center")

            for _, row in df.iterrows():
                tree.insert("", "end", values=list(row))

            tree.pack(fill=tk.BOTH, expand=True)
        except mysql.connector.Error as err:
            messagebox.showerror("Database Error", f"Error: {err}", parent=dashboard)

    # Dashboard Buttons
    tk.Button(db_frame, text="View Data", command=view_data, font="Terminal", width=20).grid(row=0, column=0, padx=20, pady=20)
    tk.Button(db_frame, text="Generate Graph", command=generate_graph, font="Terminal", width=20).grid(row=0, column=1, padx=20, pady=20)
    tk.Button(db_frame, text="Back", command=dashboard.destroy, font="Terminal", width=45).grid(row=1, column=0, columnspan=2, pady=30)


# ---Signup Function ---
    def sign_up():
        signup_window = tk.Toplevel(root)
        signup_window.title("Signup")
        signup_window.state("zoomed")

    s_frame = tk.Frame(signup_window, bd=5, relief="ridge", padx=40, pady=40)
    s_frame.place(relx=0.5, rely=0.5, anchor="center")

    tk.Label(s_frame, text="Username", font="Terminal").grid(row=0, column=0, padx=10, pady=10)
    sname_entry = tk.Entry(s_frame, font="Terminal")
    sname_entry.grid(row=0, column=1, padx=10, pady=10)

    tk.Label(s_frame, text="Password", font="Terminal").grid(row=1, column=0, padx=10, pady=10)
    s_pword_entry = tk.Entry(s_frame, font="Terminal", show="*")
    s_pword_entry.grid(row=1, column=1, padx=10, pady=10)

    tk.Label(s_frame, text="Role", font="Terminal").grid(row=2, column=0, padx=10, pady=10)
    s_role_entry = tk.StringVar(s_frame)
    s_role_entry.set("Analyst")
    role_options = ["Analyst", "Manager", "CEO"]
    role_menu = tk.OptionMenu(s_frame, s_role_entry, *role_options)
    role_menu.grid(row=2, column=1, padx=10, pady=10)

    def signup_page():
        username = sname_entry.get()
        password = s_pword_entry.get()
        role = s_role_entry.get()

        if not username or not password:
            messagebox.showerror("Error", "Please fill in all fields", parent=s_frame)
            return

        try:
            conn = mysql.connector.connect(host='localhost', user='root', password='1234', database='sales_prediction')
            cursor = conn.cursor()
            query = "INSERT INTO users (username, password, role) VALUES (%s, %s, %s)"
            cursor.execute(query, (username, password, role))
            conn.commit()
            conn.close()

            messagebox.showinfo("Signup", "Signup Successfully Completed", parent=s_frame)
            signup_window.destroy()
        except mysql.connector.Error as err:
            messagebox.showerror("Database Error", f"Error: {err}", parent=s_frame)

    tk.Button(s_frame, text="Signup", command=signup_page, font="Terminal").grid(row=3, column=0, columnspan=2, pady=20)


# --- Login Function ---
    def login():
      username = user_entry.get()
      password = pword_entry.get()

    try:
        conn = mysql.connector.connect(host='localhost', user='root', password='1234', database='sales_prediction')
        cursor = conn.cursor()
        cursor.execute("SELECT * FROM users WHERE username=%s AND password=%s", (username, password))
        result = cursor.fetchone()
        conn.close()

        if result:
            messagebox.showinfo("Login", "Login Successful")
            open_dashboard()
        else:
            messagebox.showerror("Error", "Invalid Credentials")
    except mysql.connector.Error as err:
        messagebox.showerror("Database Error", f"Error: {err}")


# --- Main GUI ---
    root = tk.Tk()
    root.state("zoomed")
    root.title("Sales Prediction System")
    root.configure(bg="black")
    
    frame = tk.Frame(root, bd=5, relief="ridge", padx=40, pady=40)
    frame.place(relx=0.5, rely=0.5, anchor="center")
    tk.Label(frame, text="Username", font="Terminal").grid(row=0, column=0, padx=10, pady=10)
    
    user_entry = tk.Entry(frame, font="Terminal")
    user_entry.grid(row=0, column=1, padx=10, pady=10)
    
    tk.Label(frame, text="Password", font="Terminal").grid(row=1, column=0, padx=10, pady=10)
    pword_entry = tk.Entry(frame, show='*', font="Terminal")
    pword_entry.grid(row=1, column=1, padx=10, pady=10)

    tk.Button(frame, text="Login", command=login, font="Terminal").grid(row=2, column=0, padx=10, pady=20)
    tk.Button(frame, text="Signup", command=sign_up, font="Terminal").grid(row=2, column=1, padx=10, pady=20)

    root.mainloop()

