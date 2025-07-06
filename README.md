-- 🏗 Step 1: Create tables

CREATE TABLE departments (
    department_id INTEGER PRIMARY KEY,
    department_name TEXT
);

CREATE TABLE employees (
    employee_id INTEGER PRIMARY KEY,
    name TEXT,
    department_id INTEGER,
    salary INTEGER
);

-- 📥 Step 2: Insert sample data

INSERT INTO departments (department_id, department_name) VALUES
(101, 'HR'),
(102, 'IT'),
(103, 'Sales');

INSERT INTO employees (employee_id, name, department_id, salary) VALUES
(1, 'Alice', 101, 80000),
(2, 'Bob', 102, 60000),
(3, 'Charlie', 101, 75000),
(4, 'David', 103, 50000),
(5, 'Emma', 102, 90000);

-- 🔍 View 1: Basic View of high-salary employees

CREATE VIEW high_salary_employees AS
SELECT name, salary
FROM employees
WHERE salary > 70000;

-- 🔍 View 2: Join View of employees with department names

CREATE VIEW employee_details AS
SELECT e.employee_id, e.name, d.department_name, e.salary
FROM employees AS e
JOIN departments AS d ON e.department_id = d.department_id;

-- 🔍 View 3: Department-wise average salary

CREATE VIEW department_avg_salary AS
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;

-- 🔍 Using a view: Show IT department employees from employee_details

SELECT *
FROM employee_details
WHERE department_name = 'IT';

-- 🧹 Drop a view

-- DROP VIEW high_salary_employees;

-- Optional: WITH CHECK OPTION (only supported in some RDBMS like MySQL)

-- CREATE VIEW editable_it_employees AS
-- SELECT * FROM employees WHERE department_id = 102
-- WITH CHECK OPTION;
