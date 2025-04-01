# DBMS-EP3-SQL

# Table: employees
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary INT
);
```

## Insert sample values into employees table
```sql
INSERT INTO employees (employee_id, name, department, salary) VALUES 
(1, 'Alice', 'HR', 50000),
(2, 'Bob', 'IT', 60000),
(3, 'Charlie', 'IT', 55000),
(4, 'David', 'Sales', NULL),
(5, 'Emma', 'HR', 56000);
```

# Count Queries
## Count non-null salary entries
``` sql
SELECT count(salary) FROM employees;
```

## Count total number of employees
``` sql
SELECT count(*) FROM employees;

```

## Count distinct departments
``` sql
SELECT count(distinct department) FROM employees;
```

# Group By Queries
## Group employees by department and count the number of employees in each department
``` sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

# SUM Queries
## Total salary of all employees

``` sql
SELECT SUM(salary) AS total_salary FROM employees;
```

## Total salary by department
``` sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

## Having Queries
## Departments with a total salary greater than 110000
``` sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 110000;
```

``` sql

```
