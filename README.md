# Vehicle Rental System – Database Design & SQL Queries

## 📌 Project Overview
The Vehicle Rental System is a relational database project designed to manage vehicle rentals efficiently.  
It stores information about users, vehicles, and bookings, and supports real-world rental operations such as booking vehicles, tracking availability, and calculating rental usage.

This project demonstrates proper database design, entity relationships, and SQL query usage including JOIN, EXISTS, WHERE, GROUP BY, and HAVING clauses.

---

## 🗂️ Database Schema
The database consists of three main tables:

### 1. Users
Stores system users such as customers and administrators.

**Attributes:**
- user_id (Primary Key)
- name
- email (Unique)
- password
- phone_number
- role (Admin / Customer)

---

### 2. Vehicles
Stores all rentable vehicles.

**Attributes:**
- vehicle_id (Primary Key)
- name
- type (car / bike / truck)
- model
- registration_number (Unique)
- rental_price
- status (available / rented / maintenance)

---

### 3. Bookings
Stores booking information connecting users and vehicles.

**Attributes:**
- booking_id (Primary Key)
- user_id (Foreign Key → Users)
- vehicle_id (Foreign Key → Vehicles)
- start_date
- end_date
- status (pending / confirmed / completed / cancelled)
- total_cost

---

## 🔗 Entity Relationships
- One user can make many bookings (One-to-Many)
- One vehicle can have many bookings over time (One-to-Many)
- Each booking is linked to exactly one user and one vehicle

---

## 🧠 Business Logic
- Each user must have a unique email
- Each vehicle must have a unique registration number
- Vehicles can only be booked if available
- Booking status tracks the rental lifecycle
- Total cost is calculated based on rental duration and daily price

---

## 🧪 SQL Queries

The project includes SQL queries that demonstrate core SQL concepts such as JOIN, NOT EXISTS, WHERE, GROUP BY, and HAVING.

---

### 🔹 Query 1: Retrieve Booking Details Using JOIN

```sql
SELECT 
    b.booking_id,
    u.name AS customer_name,
    v.name AS vehicle_name,
    b.start_date,
    b.end_date,
    b.status
FROM Bookings b
INNER JOIN Users u ON b.user_id = u.user_id
INNER JOIN Vehicles v ON b.vehicle_id = v.vehicle_id;
```
Explanation:
This query uses INNER JOIN to combine data from the Bookings, Users, and Vehicles tables.
It retrieves booking information along with the corresponding customer name and vehicle name.
Only records with matching user and vehicle IDs are returned.


### 🔹 Query 2: Find Vehicles That Have Never Been Booked (NOT EXISTS)
```sql
SELECT *
FROM Vehicles v
WHERE NOT EXISTS (
    SELECT 1
    FROM Bookings b
    WHERE b.vehicle_id = v.vehicle_id
);
```
Explanation:
This query uses the NOT EXISTS clause to identify vehicles that do not appear in the Bookings table.
It returns vehicles that have never been booked, helping to identify unused vehicles.


### 🔹 Query 3: Filter Available Vehicles Using WHERE
```sql
SELECT *
FROM Vehicles
WHERE status = 'available'
AND type = 'car';
```
Explanation:
This query filters records using the WHERE clause.
It retrieves all vehicles that are currently available and belong to a specific type, such as cars. 


### 🔹 Query 4: Aggregate Booking Data Using GROUP BY and HAVING
```sql
SELECT 
    v.name AS vehicle_name,
    COUNT(b.booking_id) AS total_bookings
FROM Vehicles v
INNER JOIN Bookings b ON v.vehicle_id = b.vehicle_id
GROUP BY v.name
HAVING COUNT(b.booking_id) > 2;
```
Explanation:
This query groups booking records by vehicle name and counts the total number of bookings for each vehicle.
The HAVING clause filters the grouped results and displays only vehicles with more than two bookings.

---
