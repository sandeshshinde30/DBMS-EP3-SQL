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

# Having Queries
## Departments with a total salary greater than 110000
``` sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 110000;
```

# Average Queries
## Average salary of all employees
``` sql
SELECT AVG(salary) AS avg_salary FROM employees;
```

## Average salary by department, only for departments with average salary greater than 50000
``` sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

## MIN Queries
## Minimum salary of all employees
``` sql
SELECT MIN(salary) AS min_salary FROM employees;
```

## Minimum salary by department, only for departments with a minimum salary greater than 50000
``` sql
SELECT department, MIN(salary) AS min_salary
FROM employees
GROUP BY department
HAVING MIN(salary) > 50000;
```

# MAX Queries
## Maximum salary of all employees
``` sql
SELECT MAX(salary) AS max_salary FROM employees;
```

## Maximum salary by department, only for departments with a maximum salary greater than 56000
``` sql
SELECT department, MAX(salary) AS max_salary
FROM employees
GROUP BY department
HAVING MAX(salary) > 56000;
```

# Nested Queries
## Employees with salary greater than the average salary
``` sql
SELECT name, department, salary 
FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

## Find the department of employee 'Bob'
``` sql
SELECT name, department 
FROM employees 
WHERE department = (SELECT department FROM employees WHERE name = 'Bob');
```

## Find Employees Who Earn More Than the Second Lowest Salary
``` sql
SELECT name, department, salary 
FROM employees 
WHERE salary > (SELECT MIN(salary) 
                FROM employees 
                WHERE salary > (SELECT MIN(salary) FROM employees));
```


# Table: employees and departments
## Create employees table with department_id column
``` sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department_id INT
);
```

## Create departments table
``` sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);
```

## Insert data into employees table
``` sql
INSERT INTO employees (employee_id, name, department_id) VALUES 
(1, 'Alice', 101),
(2, 'Bob', 102),
(3, 'Charlie', 103),
(4, 'David', NULL);
``` 

## Insert data into departments table
``` sql
INSERT INTO departments (department_id, department_name) VALUES 
(101, 'HR'),
(102, 'IT'),
(104, 'Sales');
```

# Join Queries
## Select employees and their departments using an inner join
``` sql
SELECT employees.name, departments.department_name  
FROM employees  
INNER JOIN departments ON employees.department_id = departments.department_id;
```

## Select employees and their departments using a left join
``` sql
SELECT employees.name, departments.department_name  
FROM employees  
LEFT JOIN departments ON employees.department_id = departments.department_id;
```

## Select employees and their departments using a right join
``` sql
SELECT employees.name, departments.department_name  
FROM employees  
RIGHT JOIN departments ON employees.department_id = departments.department_id;
```

# Full Outer Join 
``` sql
SELECT employees.name, departments.department_name  
FROM employees  
FULL JOIN departments ON employees.department_id = departments.department_id;
```
# Full Outer Join with union
``` sql
SELECT employees.name, departments.department_name  
FROM employees  
LEFT JOIN departments ON employees.department_id = departments.department_id  

UNION  

SELECT employees.name, departments.department_name  
FROM employees  
RIGHT JOIN departments ON employees.department_id = departments.department_id;

```

# Self Join
## Create employees table with self-referencing manager column
``` sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department_id INT,
    manager_id INT 
);

```
## Insert initial data
```sql 
INSERT INTO employees (employee_id, name, department_id, manager_id) VALUES 
(1, 'Alice', 101, NULL), 
(2, 'Bob', 102, 1),  
(3, 'Charlie', 103, 1),  
(4, 'David', 104, 2),  
(5, 'Emma', 101, 2);  

```

## Get employee and their manager names using self join
```sql 
SELECT e1.name AS employee, e2.name AS manager  
FROM employees e1  
JOIN employees e2 ON e1.manager_id = e2.employee_id;
```



