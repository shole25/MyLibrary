# MyLibrary
-- Task 1: find the total salary for employees in department 90
select sum(salary) as total_salary
from employees
where department_id = 90;

-- Task 2: find the number of employees in each department
select department_name, count(*) as employee_count
from employees
group by department_name;

-- Task 3: count rows in departments where manager_id is null
select count(*) as null_manager_count
from departments
where manager_id is null;

-- Task 4: find the count of street addresses by country_id
select country_id, count(street_address) as address_count
from locations
group by country_id;

-- Task 5: find the difference between max and min salary in department 110
select max(salary) - min(salary) as salary_difference
from employees
where department_id = 110;

-- Task 6: find the average salary for employees with names longer than 5 characters
select avg(salary) as average_salary
from employees
where length(first_name) > 5;

-- Task 7: find departments with an average salary above 7000
select department_id
from employees
group by department_id
having avg(salary) > 7000;

-- Task 8: find the department with the highest total salary
select max(sum(salary)) as max_of_sum_salary_by_dep
from employees
group by department_id;

-- Task 9: find the count of employees hired in 2001, 2002, 2003, and 2004
select 
    sum(case when extract(year from hire_date) = 2001 then 1 else 0 end) as "2001",
    sum(case when extract(year from hire_date) = 2002 then 1 else 0 end) as "2002",
    sum(case when extract(year from hire_date) = 2003 then 1 else 0 end) as "2003",
    sum(case when extract(year from hire_date) = 2004 then 1 else 0 end) as "2004"
from employees;

-- Task 10: count unique managers in each department
select department_id, count(distinct manager_id) as unique_managers_count
from employees
group by department_id;

-- Task 11: find the number of employees hired each year per department
select department_id, extract(year from hire_date) as hire_year, count(*) as hire_count
from employees
group by department_id, extract(year from hire_date);

-- Task 12: find job_ids with 20 or more employees
select job_id, count(*) as employee_count
from employees
group by job_id
having count(*) >= 20;

-- Task 13: count lowercase letters in each street_address and group by this count
select length(regexp_replace(street_address, '[^a-z]', '', 'g')) as lowercase_count, 
       count(*) as row_count
from locations
group by lowercase_count;
