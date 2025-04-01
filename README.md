# DBMS-EP3-SQL

# SQL Queries for Employees and Departments

This README file includes various SQL queries designed to manipulate and extract data from the `employees` and `departments` tables. The queries cover basic SQL operations, aggregation, joins, and nested queries.

## Table: employees

The `employees` table stores information about employees, including their employee ID, name, department, and salary.

```sql
-- Create employees table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary INT
);

-- Insert sample values
INSERT INTO employees (employee_id, name, department, salary) VALUES 
(1, 'Alice', 'HR', 50000),
(2, 'Bob', 'IT', 60000),
(3, 'Charlie', 'IT', 55000),
(4, 'David', 'Sales', NULL),
(5, 'Emma', 'HR', 56000);
