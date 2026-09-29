# 🏥 Hospital Management System

A complete **Hospital Management System using MySQL** designed to manage patients, doctors, appointments, medical records, billing, departments, and doctor-department relationships.

This project demonstrates practical use of **SQL Database Management, CRUD Operations, SQL Clauses, Operators, Joins, Aggregate Functions, Sorting, Grouping, and Constraints**.

---

## 📌 Project Overview

The **Hospital Management System** stores and manages hospital-related information in a structured relational database.

The system contains:

* 👤 Patient Management
* 👨‍⚕️ Doctor Management
* 📅 Appointment Management
* 🩺 Medical Records
* 💰 Billing Management
* 🏢 Department Management
* 🔗 Doctor-Department Relationships
* 🔍 Data Searching and Filtering
* 📊 Sorting and Grouping
* 📈 Aggregate Data Analysis

---

## 🛠️ Technologies Used

| Technology      | Purpose                     |
| --------------- | --------------------------- |
| MySQL           | Database Management         |
| SQL             | Data Manipulation & Queries |
| MySQL Workbench | Query Execution             |
| SQLBook         | SQL Project Documentation   |

---

# 🗄️ Database Information

### Database Name

```sql
hospital_management
```

Create and select the database:

```sql
CREATE DATABASE IF NOT EXISTS hospital_management;

USE hospital_management;
```

---

# 📋 Database Tables

The project contains **7 main tables**.

### 1. Patients

Stores patient information.

Important columns:

* `patient_id` — Primary Key
* `name`
* `dob`
* `gender`
* `phone_number`
* `email`
* `address`
* `registration_date`

---

### 2. Doctors

Stores doctor information.

Important columns:

* `doctor_id` — Primary Key
* `name`
* `specialization`
* `phone_number`
* `email`
* `available_days`
* `consultation_fee`

---

### 3. Appointments

Stores appointments between patients and doctors.

Important columns:

* `appointment_id` — Primary Key
* `patient_id` — Foreign Key
* `doctor_id` — Foreign Key
* `appointment_date`
* `status`

Appointment status can be:

```text
Scheduled
Completed
Cancelled
```

---

### 4. Medical_Records

Stores patient medical information.

Important columns:

* `record_id` — Primary Key
* `patient_id` — Foreign Key
* `doctor_id` — Foreign Key
* `diagnosis`
* `prescription`
* `treatment_date`

---

### 5. Billing

Stores hospital billing information.

Important columns:

* `invoice_id` — Primary Key
* `patient_id` — Foreign Key
* `appointment_id` — Foreign Key
* `amount`
* `payment_status`
* `payment_date`

Payment status:

```text
Paid
Pending
Cancelled
```

---

### 6. Departments

Stores hospital department information.

Important columns:

* `department_id` — Primary Key
* `department_name`

Examples:

```text
Cardiology
Neurology
Pediatrics
Psychiatry
General Practice
General Surgery
```

---

### 7. Doctor_Department

Connects doctors with departments.

Important columns:

* `doctor_id` — Foreign Key
* `department_id` — Foreign Key

The combination of both columns forms a **Composite Primary Key**.

---

# 🔗 Database Relationships

The database uses **Primary Keys and Foreign Keys** to establish relationships.

```text
Patients
   │
   ├──── Appointments ──── Doctors
   │
   ├──── Medical_Records ─ Doctors
   │
   └──── Billing ───────── Appointments

Doctors
   │
   └──── Doctor_Department ─── Departments
```

### Relationship Examples

```text
Patients → Appointments
Doctors → Appointments
Patients → Medical_Records
Doctors → Medical_Records
Patients → Billing
Appointments → Billing
Doctors → Departments
```

---

# 🔑 SQL Constraints Used

The project demonstrates several SQL constraints.

### PRIMARY KEY

Uniquely identifies each record.

```sql
patient_id INT PRIMARY KEY
```

### FOREIGN KEY

Creates a relationship between tables.

```sql
FOREIGN KEY (patient_id)
REFERENCES Patients(patient_id)
```

### NOT NULL

Prevents empty values.

```sql
name VARCHAR(100) NOT NULL
```

### DEFAULT

Automatically provides a value when no value is supplied.

```sql
registration_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

### CHECK

Restricts values to valid options.

```sql
CHECK (status IN ('Scheduled', 'Completed', 'Cancelled'))
```

---

# 📝 CRUD Operations

CRUD means:

* **C** — Create
* **R** — Read
* **U** — Update
* **D** — Delete

---

## ➕ CREATE / INSERT

New patients, doctors, and appointments can be added.

Example:

```sql
INSERT INTO Patients
(patient_id, name, dob, gender, phone_number, email, address)
VALUES
(21, 'Clark Kent', '1980-06-18', 'Male',
 '555-0121', 'clark.k@email.com', 'Smallville');
```

---

## 🔎 READ / SELECT

Retrieve records from tables.

```sql
SELECT * FROM Patients;
```

```sql
SELECT * FROM Doctors;
```

```sql
SELECT * FROM Appointments;
```

---

## ✏️ UPDATE

Patient information can be updated when details change.

```sql
UPDATE Patients
SET address = 'Mumbai, Maharashtra'
WHERE patient_id = 1;
```

---

## 🗑️ DELETE

Cancelled appointments older than six months can be removed.

```sql
DELETE FROM Appointments
WHERE status = 'Cancelled'
AND appointment_date < NOW() - INTERVAL 6 MONTH;
```

---

# 🔍 SQL Clauses Used

The project demonstrates:

* `WHERE`
* `ORDER BY`
* `GROUP BY`
* `LIMIT`
* `JOIN`
* `HAVING`
* `DISTINCT`

Example:

```sql
SELECT *
FROM Patients
WHERE gender = 'Female';
```

---

# ⚙️ SQL Operators

### AND

Both conditions must be true.

```sql
SELECT *
FROM Appointments
WHERE status = 'Scheduled'
AND doctor_id = 10;
```

### OR

At least one condition must be true.

```sql
SELECT *
FROM Doctors
WHERE specialization = 'Cardiology'
OR specialization = 'Neurology';
```

### NOT

Excludes a condition.

```sql
SELECT *
FROM Doctors
WHERE NOT specialization = 'Cardiology';
```

### IN

Checks multiple values.

```sql
SELECT *
FROM Doctors
WHERE specialization IN ('Cardiology', 'Neurology');
```

### NOT IN

Excludes multiple values.

```sql
SELECT *
FROM Doctors
WHERE specialization NOT IN ('Cardiology', 'Neurology');
```

### Comparison Operators

The project can use:

```text
=
>
<
>=
<=
<>
```

Example:

```sql
SELECT *
FROM Doctors
WHERE consultation_fee > 100;
```

---

# 🔗 SQL JOINS

Joins combine data from multiple tables.

### INNER JOIN

Example: Retrieve doctors with their department names.

```sql
SELECT
    d.doctor_id,
    d.name AS doctor_name,
    dept.department_name
FROM Doctors d
INNER JOIN Doctor_Department dd
    ON d.doctor_id = dd.doctor_id
INNER JOIN Departments dept
    ON dd.department_id = dept.department_id;
```

### Patient + Appointment

```sql
SELECT
    p.name AS patient_name,
    a.appointment_date,
    a.status
FROM Patients p
INNER JOIN Appointments a
    ON p.patient_id = a.patient_id;
```

### Doctor + Appointment

```sql
SELECT
    d.name AS doctor_name,
    a.appointment_date,
    a.status
FROM Doctors d
INNER JOIN Appointments a
    ON d.doctor_id = a.doctor_id;
```

---

# 📊 Sorting and Grouping

## ORDER BY

Doctors can be sorted by specialization.

```sql
SELECT *
FROM Doctors
ORDER BY specialization ASC;
```

For descending order:

```sql
SELECT *
FROM Doctors
ORDER BY consultation_fee DESC;
```

---

## GROUP BY

Count patients assigned to each doctor.

```sql
SELECT
    doctor_id,
    COUNT(patient_id) AS total_patients
FROM Appointments
GROUP BY doctor_id;
```

---

# 📈 Aggregate Functions

The project uses aggregate functions for data analysis.

### COUNT()

```sql
SELECT COUNT(*) AS total_patients
FROM Patients;
```

### SUM()

```sql
SELECT SUM(amount) AS total_revenue
FROM Billing
WHERE payment_status = 'Paid';
```

### AVG()

```sql
SELECT AVG(consultation_fee) AS average_fee
FROM Doctors;
```

### MAX()

```sql
SELECT MAX(consultation_fee) AS highest_fee
FROM Doctors;
```

### MIN()

```sql
SELECT MIN(consultation_fee) AS lowest_fee
FROM Doctors;
```

---

# 📌 Important Queries

### Total Revenue

```sql
SELECT SUM(amount) AS total_revenue
FROM Billing
WHERE payment_status = 'Paid';
```

### Average Consultation Fee

```sql
SELECT AVG(consultation_fee) AS average_consultation_fee
FROM Doctors;
```

### Most Visited Doctor

```sql
SELECT
    d.name AS doctor_name,
    COUNT(a.appointment_id) AS total_visits
FROM Doctors d
JOIN Appointments a
    ON d.doctor_id = a.doctor_id
GROUP BY d.doctor_id, d.name
ORDER BY total_visits DESC
LIMIT 1;
```

### Total Revenue Per Department

```sql
SELECT
    dept.department_name,
    SUM(b.amount) AS total_revenue
FROM Billing b
JOIN Appointments a
    ON b.appointment_id = a.appointment_id
JOIN Doctors d
    ON a.doctor_id = d.doctor_id
JOIN Doctor_Department dd
    ON d.doctor_id = dd.doctor_id
JOIN Departments dept
    ON dd.department_id = dept.department_id
WHERE b.payment_status = 'Paid'
GROUP BY dept.department_id, dept.department_name;
```

---

# 🧮 DISTINCT

`DISTINCT` is used to remove duplicate values from query results.

Example:

```sql
SELECT DISTINCT specialization
FROM Doctors;
```

This returns each specialization only once.

---

# 📅 Date Operations

The project uses MySQL date functions.

Example: Patients registered during the last year.

```sql
SELECT
    patient_id,
    name,
    registration_date
FROM Patients
WHERE registration_date >= NOW() - INTERVAL 1 YEAR
ORDER BY registration_date DESC;
```

---

# 📌 Project Features

✅ Patient Management
✅ Doctor Management
✅ Appointment Scheduling
✅ Medical Records
✅ Billing Management
✅ Department Management
✅ Foreign Key Relationships
✅ CRUD Operations
✅ SQL Operators
✅ SQL Clauses
✅ INNER JOIN
✅ GROUP BY
✅ ORDER BY
✅ Aggregate Functions
✅ Date Filtering
✅ Data Searching
✅ Data Sorting
✅ Data Analysis

---

# ▶️ How to Run the Project

### Step 1

Open **MySQL Workbench**.

### Step 2

Connect to your MySQL Server.

### Step 3

Open the SQLBook / SQL file.

### Step 4

Run:

```sql
CREATE DATABASE IF NOT EXISTS hospital_management;

USE hospital_management;
```

### Step 5

Execute the table creation queries in order:

```text
Patients
Doctors
Appointments
Medical_Records
Billing
Departments
Doctor_Department
```

### Step 6

Execute the INSERT queries.

### Step 7

Run SELECT queries to verify the data.

```sql
SELECT * FROM Patients;
SELECT * FROM Doctors;
SELECT * FROM Appointments;
SELECT * FROM Medical_Records;
SELECT * FROM Billing;
SELECT * FROM Departments;
SELECT * FROM Doctor_Department;
```

---

# 📂 Project Structure

```text
Hospital-Management-System/
│
├── hospital management system.sqlbook
└── README.md
```

---

# 🎯 Learning Objectives

This project helps demonstrate practical knowledge of:

* Relational Database Management
* MySQL
* SQL Syntax
* Database Design
* Primary and Foreign Keys
* Constraints
* CRUD Operations
* SQL Operators
* SQL Clauses
* Joins
* Aggregate Functions
* Sorting and Grouping
* Date Functions
* Data Analysis

---

# ⚠️ Important Note

The database is intended as an **educational SQL project** for practicing MySQL concepts such as database design, relationships, queries, constraints, CRUD operations, and data analysis.

---

## 👩‍💻 Author

**Khevna Goyani**

---

## ⭐ Project

**Hospital Management System using MySQL**

A practical SQL database project demonstrating how a hospital's major operations can be organized using a relational database.

