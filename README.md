# 📊 End-to-End ETL Pipeline: Excel to PostgreSQL

## 📌 Project Overview
⭐ Built as part of my Data Engineering learning journey.

This project demonstrates a structured **ETL (Extract, Transform, Load)** pipeline built using **Python (Pandas)** and **PostgreSQL (Supabase)**.

The pipeline extracts structured data from Excel files, performs data cleaning and transformation, and loads the cleaned data into a relational PostgreSQL database with enforced primary and foreign key constraints.

The goal of this project was to deeply understand ETL fundamentals, relational modeling, and safe full-refresh loading strategies.

---

## 🏗 Architecture

**Source:**  
Excel files  
- Customers  
- Orders  
- Employees  

**Processing Layer:**  
Python + Pandas  

**Target System:**  
PostgreSQL (Supabase)

---

## 🔄 ETL Workflow

### 1️⃣ Extract
- Read structured Excel datasets using Pandas

### 2️⃣ Transform
- Convert Zipcode to string
- Remove duplicate business keys (Email)
- Handle null values
- Clean currency fields (remove `$`, convert to numeric)
- Convert date columns to datetime
- Drop irrelevant columns

### 3️⃣ Load
- Full refresh strategy using `TRUNCATE + append`
- Maintain relational constraints
- Ensure clean and consistent table state

---

## 🗄 Database Design

### Customers
- `CustomerID` (Primary Key)
- FirstName
- LastName
- Email
- Phone
- Address
- City
- State
- Zipcode

### Orders
- `OrderID` (Primary Key)
- Date
- TotalDue
- Status
- `CustomerID` (Foreign Key → Customers)

### Employees
- `EmployeeID` (Surrogate Key)
- Employee Name
- Department
- Salary
- Benefits
- Other cleaned attributes

---

## 🔐 Relational Integrity

- Primary Key: `customers(CustomerID)`
- Primary Key: `orders(OrderID)`
- Foreign Key: `orders(CustomerID)` → `customers(CustomerID)`

The pipeline uses `TRUNCATE TABLE ... CASCADE` to safely refresh parent-child tables while preserving database structure and constraints.

---

## ⚙ Tech Stack

- Python
- Pandas
- SQLAlchemy
- PostgreSQL (Supabase)
- Jupyter Notebook

---

## 🧠 Key Learnings

- Building ETL pipelines from scratch
- Data type standardization and transformation logic
- Business key vs surrogate key handling
- Duplicate detection and null management
- Referential integrity and foreign key behavior
- TRUNCATE vs DROP differences
- Full refresh vs incremental load strategies
- Safe database transaction handling using context managers

---

## 🚀 How to Run

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Update the PostgreSQL connection string in the notebook.

3. Run the notebook cells in order.

---

## 📂 Project Structure

```
etl-postgres-project/
│
├── ETL_Final.ipynb
├── data/
│   ├── H+ Sport Customers.xlsx
│   ├── H+ Sport Orders.xlsx
│   └── H+ Sport Employees.xlsx
├── requirements.txt
└── README.md
```

---

## 🎯 Project Objective

This project was built to strengthen practical understanding of structured ETL pipelines and relational database integrity, moving beyond basic data cleaning toward production-oriented thinking.
