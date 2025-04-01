# DBMS-EP3-SQL

-- Create employees table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary INT
);

-- Insert sample values into employees table
INSERT INTO employees (employee_id, name, department, salary) VALUES 
(1, 'Alice', 'HR', 50000),
(2, 'Bob', 'IT', 60000),
(3, 'Charlie', 'IT', 55000),
(4, 'David', 'Sales', NULL),
(5, 'Emma', 'HR', 56000);

-- Count non-null salary entries
SELECT count(salary) FROM employees;

-- Count total number of employees
SELECT count(*) FROM employees;

-- Count distinct departments
SELECT count(distinct department) FROM employees;

-- Group employees by department and count the number of employees in each department
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;

-- Total salary of all employees
SELECT SUM(salary) AS total_salary FROM employees;

-- Total salary by department
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;

-- Departments with a total salary greater than 110000
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 110000;

-- Average salary of all employees
SELECT AVG(salary) AS avg_salary FROM employees;

-- Average salary by department, only for departments with average salary greater than 50000
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;

-- Minimum salary of all employees
SELECT MIN(salary) AS min_salary FROM employees;

-- Minimum salary by department, only for departments with a minimum salary greater than 50000
SELECT department, MIN(salary) AS min_salary
FROM employees
GROUP BY department
HAVING MIN(salary) > 50000;

-- Maximum salary of all employees
SELECT MAX(salary) AS max_salary FROM employees;

-- Maximum salary by department, only for departments with a maximum salary greater than 56000
SELECT department, MAX(salary) AS max_salary
FROM employees
GROUP BY department
HAVING MAX(salary) > 56000;

-- Employees with salary greater than the average salary
SELECT name, department, salary 
FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Find the department of employee 'Bob'
SELECT name, department 
FROM employees 
WHERE department = (SELECT department FROM employees WHERE name = 'Bob');

-- Employees with a salary greater than the average salary in their department
SELECT name, department, salary 
FROM employees e1
WHERE salary > (SELECT AVG(salary) 
                FROM employees e2 
                WHERE e1.department = e2.department);

-- Create employees table with department_id column
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department_id INT
);

-- Create departments table
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);

-- Insert data into employees table
INSERT INTO employees (employee_id, name, department_id) VALUES 
(1, 'Alice', 101),
(2, 'Bob', 102),
(3, 'Charlie', 103),
(4, 'David', NULL);

-- Insert data into departments table
INSERT INTO departments (department_id, department_name) VALUES 
(101, 'HR'),
(102, 'IT'),
(104, 'Sales');

-- Select employees and their departments using an inner join
SELECT employees.name, departments.department_name  
FROM employees  
INNER JOIN departments ON employees.department_id = departments.department_id;

-- Select employees and their departments using a left join
SELECT employees.name, departments.department_name  
FROM employees  
LEFT JOIN departments ON employees.department_id = departments.department_id;

-- Select employees and their departments using a right join
SELECT employees.name, departments.department_name  
FROM employees  
RIGHT JOIN departments ON employees.department_id = departments.department_id;

-- Full outer join simulation using union
SELECT employees.name, departments.department_name  
FROM employees  
LEFT JOIN departments ON employees.department_id = departments.department_id  

UNION  

SELECT employees.name, departments.department_name  
FROM employees  
RIGHT JOIN departments ON employees.department_id = departments.department_id;

-- Create employees table with self-referencing manager column
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department_id INT,
    manager_id INT  -- Self-referencing column for managers
);

-- Insert initial data
INSERT INTO employees (employee_id, name, department_id, manager_id) VALUES 
(1, 'Alice', 101, NULL),  -- Alice has no manager (top-level)
(2, 'Bob', 102, 1),  -- Bob reports to Alice
(3, 'Charlie', 103, 1),  -- Charlie reports to Alice
(4, 'David', 104, 2),  -- David reports to Bob
(5, 'Emma', 101, 2);  -- Emma reports to Bob

-- Get employee and their manager names using self join
SELECT e1.name AS employee, e2.name AS manager  
FROM employees e1  
JOIN employees e2 ON e1.manager_id = e2.employee_id;
