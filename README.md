# PRECTICAL-SQL-hospital_management-
# 🏥 Hospital Management System — MySQL

> A complete relational database project designed to manage patients, doctors, appointments, medical records, billing, and hospital departments using **MySQL**.

---

## 📌 Project Overview

The **Hospital Management System** is a MySQL-based database project that organizes important hospital information into structured and related tables.

The project demonstrates practical SQL concepts such as:

* Database & Table Creation
* Primary Keys
* Foreign Keys
* CRUD Operations
* INNER JOIN
* CROSS JOIN
* SELF JOIN
* ORDER BY
* GROUP BY
* Aggregate Functions
* Constraints
* Data Filtering
* Relationships between tables

---

## 🎯 Project Objectives

The main objectives of this project are:

1. Manage patient information.
2. Store doctor and specialization details.
3. Schedule and track appointments.
4. Maintain medical records.
5. Manage hospital billing and payments.
6. Organize doctors into departments.
7. Establish relationships between different hospital entities.
8. Perform meaningful data analysis using SQL queries.

---

## 🗂️ Database Structure

**Database Name:** `hospital_management`

### 👤 1. Patients

Stores basic information about hospital patients.

| Column            | Description            |
| ----------------- | ---------------------- |
| patient_id        | Unique patient ID      |
| name              | Patient name           |
| dob               | Date of birth          |
| gender            | Gender                 |
| phone_number      | Contact number         |
| email             | Email address          |
| address           | Patient address        |
| registration_date | Registration timestamp |

---

### 👨‍⚕️ 2. Doctors

Stores information about doctors.

| Column           | Description            |
| ---------------- | ---------------------- |
| doctor_id        | Unique doctor ID       |
| name             | Doctor name            |
| specialization   | Medical specialization |
| phone_number     | Contact number         |
| email            | Email address          |
| available_days   | Available working days |
| consultation_fee | Consultation charges   |

---

### 📅 3. Appointments

Connects patients with doctors for appointments.

| Column           | Description                       |
| ---------------- | --------------------------------- |
| appointment_id   | Unique appointment ID             |
| patient_id       | Related patient                   |
| doctor_id        | Related doctor                    |
| appointment_date | Appointment date & time           |
| status           | Scheduled / Completed / Cancelled |

---

### 🩺 4. Medical Records

Stores diagnosis, prescription, and treatment information.

| Column         | Description              |
| -------------- | ------------------------ |
| record_id      | Unique medical record ID |
| patient_id     | Related patient          |
| doctor_id      | Related doctor           |
| diagnosis      | Patient diagnosis        |
| prescription   | Prescribed treatment     |
| treatment_date | Treatment date           |

---

### 💳 5. Billing

Manages invoices and payment information.

| Column         | Description                |
| -------------- | -------------------------- |
| invoice_id     | Unique invoice ID          |
| patient_id     | Related patient            |
| appointment_id | Related appointment        |
| amount         | Billing amount             |
| payment_status | Paid / Pending / Cancelled |
| payment_date   | Payment date               |

---

### 🏢 6. Departments

Stores hospital department information.

Examples:

* Cardiology
* Internal Medicine
* Endocrinology
* Psychiatry
* Neurology
* General Practice
* General Surgery
* Diagnostic Medicine
* Pediatrics
* Orthopedics

---

### 🔗 7. Doctor_Department

This is a **junction table** that connects doctors with departments.

It uses a **composite primary key**:

```sql
PRIMARY KEY (doctor_id, department_id)
```

---

## 🔗 Table Relationships

```text
Patients
   │
   ├────────── Appointments ────────── Doctors
   │                    │
   │                    │
   └──────── Medical_Records ─────────┘
   │
   └────────── Billing
                    │
                    └── Appointments

Doctors ───── Doctor_Department ───── Departments
```

---

## 🛠️ Technologies Used

* **MySQL**
* **MySQL Workbench**
* **SQL**
* **Relational Database Concepts**

---

## 💡 SQL Concepts Demonstrated

### Database Management

```sql
CREATE DATABASE
USE
CREATE TABLE
```

### Data Manipulation

```sql
INSERT INTO
SELECT
UPDATE
DELETE
```

### Constraints

```sql
PRIMARY KEY
FOREIGN KEY
REFERENCES
CHECK
NOT NULL
DEFAULT
```

### Data Analysis

```sql
COUNT()
SUM()
AVG()
MIN()
MAX()
```

### Query Operations

```sql
WHERE
AND
OR
IN
NOT IN
DISTINCT
ORDER BY
GROUP BY
```

### Joins

```sql
INNER JOIN
CROSS JOIN
SELF JOIN
```

---

## 📊 Example Analysis Questions

This database can be used to answer questions such as:

* How many patients are registered?
* How many doctors work in each specialization?
* Which doctors have the highest consultation fees?
* How many patients are assigned to each doctor?
* What is the total revenue generated?
* What is the average consultation fee?
* Which doctor has the most appointments?
* Which appointments are completed?
* Which invoices are pending?
* Which doctors belong to each department?
* Retrieve doctors along with their department names.
* Link medical records with the correct patients and doctors.

---

## ▶️ How to Run the Project

### Step 1 — Open MySQL Workbench

Open **MySQL Workbench** and connect to your MySQL server.

### Step 2 — Open the SQL file

Open the project SQL file:

```text
hospital managment system.sqlbook
```

### Step 3 — Execute the Database Creation

Run:

```sql
CREATE DATABASE IF NOT EXISTS hospital_management;

USE hospital_management;
```

### Step 4 — Create Tables

Execute the table creation and insertion queries in order:

```text
1. Patients
2. Doctors
3. Appointments
4. Medical_Records
5. Billing
6. Departments
7. Doctor_Department
```

### Step 5 — Verify the Database

```sql
SHOW DATABASES;

USE hospital_management;

SHOW TABLES;
```

---

## 🔍 Sample Query

### Retrieve Doctors with Their Department Names

```sql
SELECT 
    d.name AS Doctor_Name,
    d.specialization,
    dept.department_name
FROM Doctors d
INNER JOIN Doctor_Department dd
    ON d.doctor_id = dd.doctor_id
INNER JOIN Departments dept
    ON dd.department_id = dept.department_id;
```

---

## 📈 Project Benefits

This project provides practical experience with:

* Relational database design
* Data integrity
* Table relationships
* SQL query writing
* Healthcare data organization
* Data analysis
* Database management

---

## 📁 Project Structure

```text
Hospital-Management-System/
│
├── hospital managment system.sqlbook
└── README.md
```

---

## 🎓 Learning Outcome

After completing this project, you will understand how to design and manage a relational database and use SQL to store, retrieve, connect, filter, group, and analyze hospital-related data.

---

## 👩‍💻 Author

**Khevna Goyani**

---

## ⭐ Project

A practical SQL project created for learning and demonstrating **MySQL Database Management and Relational SQL Concepts**.

---
