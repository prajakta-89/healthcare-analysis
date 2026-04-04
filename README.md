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
