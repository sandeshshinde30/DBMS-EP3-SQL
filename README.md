# DBMS-EP3-SQL

## Table: employees
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary INT
);

## Insert sample values into employees table
INSERT INTO employees (employee_id, name, department, salary) VALUES 
(1, 'Alice', 'HR', 50000),
(2, 'Bob', 'IT', 60000),
(3, 'Charlie', 'IT', 55000),
(4, 'David', 'Sales', NULL),
(5, 'Emma', 'HR', 56000);

