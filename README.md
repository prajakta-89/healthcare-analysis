# healthcare-analysis
Healthcare Data Analysis using SQL. This project demonstrates how healthcare data can be leveraged to improve efficiency,
reduce costs, and enhance patient care.

# 🏥 Healthcare Analytics using SQL

## Project Overview
This project focuses on analyzing healthcare data using SQL to extract meaningful insights that improve hospital operations, patient care, and overall efficiency.

The analysis is entirely performed using SQL queries, demonstrating strong data querying, transformation, and analytical skills.

## 🎯 Business Problem
Healthcare institutions often face challenges such as:
- High patient wait times  
- Uneven distribution of workload among doctors  
- Rising treatment costs  
- Lack of data-driven decision making  

Without proper analysis, these issues impact both patient satisfaction and hospital efficiency.

## 🎯 Objective
- Analyze healthcare data using SQL  
- Identify operational inefficiencies  
- Evaluate doctor and department performance  
- Provide actionable insights for improvement  

## Tools & Technologies
- SQL (MySQL)  
- Database Tables (Patients, Doctors, Appointments, Bills, Departments) 

## Dataset Description
The dataset consists of multiple tables:

### 🧑‍⚕️ Patients
- patient_id  
- patient_name  
- age  
- gender  

### 👨‍⚕️ Doctors
- doctor_id  
- doctor_name  
- department_id  

### 🏥 Departments
- department_id  
- department_name  

### 📅 Appointments
- appointment_id  
- patient_id  
- doctor_id  
- appointment_date  
- status  

### 💰 Bills
- bill_id  
- patient_id  
- doctor_id  
- amount  
- bill_date
  
## 🧹 Data Cleaning & Preparation
- Handled missing/null values  
- Ensured data consistency across tables  
- Removed duplicate records  
- Standardized date formats  
- Validated relationships using JOINs  

## 📊 SQL Analysis Performed

### 1. Total Patients
```sql
SELECT COUNT(*) AS total_patients FROM patients;
```
### 2. List the first 10 patients from the city ‘Bengaluru’, showing patient_id, full name, city, and blood group.

```sql
SELECT
    patient_id,
    CONCAT(first_name, ' ', last_name) AS full_name,
    city,
    blood_group
FROM patients
WHERE city = 'Bengaluru'
LIMIT 10;
```
### 3. Display all doctors who are currently ‘Active’ and have more than 10 years of experience.
```sql
SELECT
    doctor_id,
    first_name,
    last_name,
    specialization,
    experience_years
FROM doctors
WHERE status = 'Active'
  AND experience_years > 10;
```
### 4. Find the total number of patients treated by each doctor.
Display doctor_id, doctor name, and patient_count.
```sql
SELECT
    d.doctor_id,
    CONCAT(d.first_name, ' ', d.last_name) AS doctor_name,
    COUNT(DISTINCT a.patient_id) AS patient_count
FROM doctors d
JOIN appointments a
    ON d.doctor_id = a.doctor_id
GROUP BY d.doctor_id, d.first_name, d.last_name;
```
### 5.For each payment mode, find how many bills are ‘Paid’ and their total net_amount.
```sql
SELECT
    payment_mode,
    COUNT(*) AS paid_bill_count,
    SUM(net_amount) AS total_net_amount
FROM bills
WHERE payment_status = 'Paid'
GROUP BY payment_mode;
```
### 6. Show top 5 departments with the highest total revenue generated from patient bills.
```sql
SELECT
    dep.department_id,
    dep.department_name,
    SUM(b.net_amount) AS total_revenue
FROM departments dep
JOIN doctors d
    ON dep.department_id = d.department_id
JOIN bills b
    ON d.doctor_id = b.doctor_id
WHERE b.payment_status = 'Paid'
GROUP BY dep.department_id, dep.department_name
ORDER BY total_revenue DESC
LIMIT 5;
```
### 7. Create a view named “vw_doctor_revenue” that displays each doctor’s total revenue collected from paid bills.
The view should include:
●	Doctor ID
●	Doctor Full Name
●	Total Revenue (sum of net_amount from paid bills)
Then write a query to:
1.	Select all columns from vw_doctor_revenue.
2.	Display only those doctors whose total revenue exceeds ₹1000
```sql
CREATE VIEW vw_doctor_revenue AS
SELECT
    d.doctor_id,
    CONCAT(d.first_name, ' ', d.last_name) AS doctor_full_name,
    SUM(b.net_amount) AS total_revenue
FROM doctors d
JOIN bills b
    ON d.doctor_id = b.doctor_id
WHERE b.payment_status = 'Paid'
GROUP BY d.doctor_id, d.first_name, d.last_name;

SELECT * FROM vw_doctor_revenue;

SELECT *
FROM vw_doctor_revenue
WHERE total_revenue > 1000;
```
