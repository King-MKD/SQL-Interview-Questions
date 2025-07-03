# SQL-Interview-Questions

Q1. Second highest salary of an employee
with t1 as(
select emp_id,
max(salary) as salary
from sales
group by emp_id
),
t2 as (
select emp_id,dense_rank() over(order by salary desc) as rnk
from t1
)
select emp_id 
from
t2
where rnk=2;

Q2. Dept wise highest salary
with t1 as(
select emp_id, dept_id, rank() over(partition by dept_id order by salary desc) as rnk
from employees
)
select dept_id,emp_id 
from t1
where rnk=1

Q3. Display alt records
with t1 as(
select emp_id, salary,
row_number() over(order by salary desc) as rn
from employee)
select emp_id, salary
from t1
where rn%2!=0
