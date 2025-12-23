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

##  SQL Concepts Covered
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


CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    role VARCHAR(20) NOT NULL
        CHECK (role IN ('Admin', 'Customer'))
);

CREATE TABLE vehicles (
    vehicle_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    type VARCHAR(20) NOT NULL
        CHECK (type IN ('car', 'bike', 'truck')),
    model VARCHAR(20) NOT NULL,
    registration_number VARCHAR(50) NOT NULL UNIQUE,
    rental_price INT NOT NULL,
    status VARCHAR(20) NOT NULL
        CHECK (status IN ('available', 'rented', 'maintenance'))
);


CREATE TABLE bookings (
    booking_id SERIAL PRIMARY KEY,

    user_id INT NOT NULL REFERENCES users(user_id),
    vehicle_id INT NOT NULL REFERENCES vehicles(vehicle_id),

    start_date DATE NOT NULL,
    end_date DATE NOT NULL,

    status VARCHAR(20) NOT NULL
        CHECK (status IN ('pending', 'confirmed', 'completed', 'cancelled')),

    total_cost INT NOT NULL
);


INSERT INTO users (user_id, name, email, phone, role, password)
VALUES
(1, 'Alice', 'alice@example.com', '1234567890', 'Customer', 'alice123'),
(2, 'Bob', 'bob@example.com', '0987654321', 'Admin', 'bob123'),
(3, 'Charlie', 'charlie@example.com', '1122334455', 'Customer', 'charlie123');

INSERT INTO vehicles (name, type, model, registration_number, rental_price, status) VALUES
('Toyota Corolla', 'car', '2022', 'ABC-123', 50, 'available'),
('Honda Civic', 'car', '2021', 'DEF-456', 60, 'rented'),
('Yamaha R15', 'bike', '2023', 'GHI-789', 30, 'available'),
('Ford F-150', 'truck', '2020', 'JKL-012', 100, 'maintenance');

INSERT INTO bookings (user_id, vehicle_id, start_date, end_date, status, total_cost) VALUES
(1, 2, '2023-10-01', '2023-10-05', 'completed', 240),
(1, 2, '2023-11-01', '2023-11-03', 'completed', 120),
(3, 2, '2023-12-01', '2023-12-02', 'confirmed', 60),
(1, 1, '2023-12-10', '2023-12-12', 'pending', 100);

-- Query 1: Retrieve booking info with customer name & vehicle name
SELECT 
    b.booking_id,
    u.name AS customer_name,
    v.name AS vehicle_name,
    b.start_date,
    b.end_date,
    b.status
FROM bookings AS b
INNER JOIN users AS u
    ON b.user_id = u.user_id
INNER JOIN vehicles AS v
    ON b.vehicle_id = v.vehicle_id
ORDER BY b.booking_id;

-- Query 2: Find vehicles that have never been booked
SELECT 
    v.vehicle_id,
    v.name,
    v.type,
    v.model,
    v.registration_number,
    v.rental_price,
    v.status
FROM vehicles v
WHERE NOT EXISTS (
    SELECT 1
    FROM bookings b
    WHERE b.vehicle_id = v.vehicle_id
)
ORDER BY v.vehicle_id;
--3
SELECT 
    vehicle_id,
    name,
    type,
    model,
    registration_number,
    rental_price,
    status
FROM vehicles
WHERE type = 'car'
  AND status = 'available'
ORDER BY vehicle_id;

--4.
SELECT 
    v.name AS vehicle_name,
    COUNT(b.booking_id) AS total_bookings
FROM bookings b
INNER JOIN vehicles v
    ON b.vehicle_id = v.vehicle_id
GROUP BY v.name
HAVING COUNT(b.booking_id) > 2;

