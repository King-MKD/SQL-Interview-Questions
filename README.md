# SQL-Interview-Questions

Q1. Second highest salary of an employee

WITH t1 AS (
    SELECT emp_id,
           MAX(salary) AS salary
    FROM sales
    GROUP BY emp_id
),
t2 AS (
    SELECT emp_id,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM t1
)
SELECT emp_id
FROM t2
WHERE rnk = 2;


Q2. Dept wise highest salary

WITH t1 AS (
    SELECT 
        emp_id,
        dept_id,
        RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rnk
    FROM employees
)
SELECT dept_id, emp_id
FROM t1
WHERE rnk = 1;


Q3. Display alt records

WITH t1 AS (
    SELECT emp_id, salary,
           ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn
    FROM employee
)
SELECT emp_id, salary
FROM t1
WHERE rn % 2 != 0;

