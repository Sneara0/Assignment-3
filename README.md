# Assignment-3

# Vehicle Rental System – SQL Queries Documentation

## 📌 Project Overview
This project demonstrates the use of SQL queries on a Vehicle Rental System database.
The database consists of multiple related tables such as users, vehicles, and bookings.
The goal of this assignment is to showcase practical usage of SQL concepts including
JOIN, WHERE, EXISTS, GROUP BY, and HAVING.

---

## 🗂️ Database Tables Used

### 1. Users
Stores customer information.
- user_id
- name
- email
- role

### 2. Vehicles
Stores vehicle details.
- vehicle_id
- name
- type
- model
- registration_number
- rental_price
- status

### 3. Bookings
Stores booking records.
- booking_id
- user_id
- vehicle_id
- start_date
- end_date
- status
- total_cost

---

## 🧠 SQL Concepts Covered
- INNER JOIN
- WHERE clause
- NOT EXISTS
- GROUP BY
- HAVING
- Aggregate Functions (COUNT)

---

## 📊 Queries Explanation

### Query 1: JOIN
Retrieve booking information along with customer name and vehicle name using INNER JOIN.

### Query 2: EXISTS
Find all vehicles that have never been booked using NOT EXISTS.

### Query 3: WHERE
Retrieve all available vehicles of a specific type (e.g., car).

### Query 4: GROUP BY & HAVING
Find vehicles that have been booked more than 2 times.

---

## ✅ Conclusion
This project demonstrates how relational database tables can be queried efficiently
using SQL to extract meaningful insights for a vehicle rental system.

