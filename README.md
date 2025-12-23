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
The project includes SQL queries that demonstrate:
- Retrieving booking details using JOIN
- Finding vehicles never booked using NOT EXISTS
- Filtering vehicles using WHERE
- Aggregating booking data using GROUP BY and HAVING

All queries are provided in the `queries.sql` file.

---

## ✅ Conclusion
This project follows proper relational database principles .  
It clearly demonstrates understanding of constraints, and advanced SQL querying techniques.
