#Project: Employee Performance Mapping
#Create a database named employee, then import data_science_team.csv proj_table.csv and emp_record_table.csv into the 
#employee database from the given resources.
CREATE DATABASE EMPLOYEE;
USE EMPLOYEE;
select * from data_science_team;
select * from proj_table;
select * from emp_record_table;

#Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, 
#and make a list of employees and details of their department.
select EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT from emp_record_table group by DEPT;

#Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is: 
#less than two
select  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT,  EMP_RATING from emp_record_table where EMP_RATING < 2;
 
#greater than four 
select  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT,  EMP_RATING from emp_record_table where EMP_RATING > 4;
#between two and four
select  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT,  EMP_RATING from emp_record_table where EMP_RATING BETWEEN 2 AND 4;

#Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and 
#then give the resultant column alias as NAME.
SELECT concat(FIRST_NAME,' ', LAST_NAME) AS NAME FROM EMP_RECORD_TABLE WHERE DEPT ='FINANCE';

#Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters 
#(including the President).
Select  emp_id ,concat(first_name,' ',last_name) FROM emp_record_table where manager_id is not null;

#Write a query to list down all the employees from the healthcare and finance departments using union. 
#Take data from the employee record table.
select concat(first_name,' ',last_name),dept from emp_record_table where dept ='healthcare' union  
select concat(first_name,' ',last_name), dept from emp_record_table where dept ='finance' 

#Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING 
#grouped by dept. Also include the respective employee rating along with the max emp rating for the department.
select EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPT, EMP_RATING, EMP_RATING as  max_RATING from emp_record_table 
where (dept, emp_rating) in (select dept, max(emp_rating) from emp_record_table group by dept) order by dept asc; 

#Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.
select role ,min(salary) as minsalary , max(salary) as maxsalary from emp_record_table group by role;

#Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.
select concat(first_name,' ',last_name) , exp as experience, dense_rank() over 
(order by exp desc) as experience_rank from emp_record_table;

#Write a query to create a view that displays employees in various countries whose salary is more than six thousand.
#Take data from the employee record table.
CREATE VIEW VIEW_EMP AS SELECT  emp_id ,concat(first_name,' ',last_name),COUNTRY , salary FROM emp_record_table where salary >6000;
select * from VIEW_EMP;

#Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.
select emp_id,  concat(first_name,' ',last_name) ,exp from emp_record_table where exp in (select exp from emp_record_table where exp >10);

#Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three
#years. Take data from the employee record table.
delimiter //
create procedure stored_emp4 (in exper int) begin select  * from emp_record_table where exp > exper ; end // 
delimiter ;
call stored_emp ('4');

#Write a query using stored functions in the project table to check whether the job profile assigned to each employee in 
#the data science team matches the organization’s set standard.
#The standard being:
#For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST',
#For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',
#For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',
#For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
#For an employee with the experience of 12 to 16 years assign 'MANAGER'.
Delimiter //
create procedure stored_projec() begin 
select * FROM emp_record_table 
CASE  WHEN EXP <=2 THEN SET ROLE ='JUNIOR DATA SCIENTIST'; WHEN EXP BETWEEN 3 AND 5 THEN SET ROLE = 'ASSOCIATE DATA SCIENTIST';
    #WHEN EXP BETWEEN 6 AND 10 THEN SET ROLE = 'SENIOR DATA SCIENTIST';
	#WHEN EXP BETWEEN 11 AND 12 THEN SET ROLE = 'LEAD DATA SCIENTIST';
    #WHEN EXP BETWEEN 13 AND 16 THEN SET ROLE = 'MANAGER';ELSE SET ROLE ='ALL GOOD'; 
END CASE;END // DELIMITER ;    

#Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.
ALTER TABLE emp_record_table ADD INDEX firstname_index(FIRST_NAME);
select * from emp_record_table where FIRST_NAME ='ERIC';

#Write a query to calculate the bonus for all the employees, based on their ratings and salaries 
#(Use the formula: 5% of salary * employee rating).
SELECT concat(first_name,' ',last_name),SALARY, (SALARY * 0.05 * EMP_RATING) AS BONUS from emp_record_table ;

#Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.
SELECT AVG(SALARY) , COUNTRY  FROM emp_record_table GROUP BY COUNTRY ORDER BY COUNTRY;
SELECT AVG(SALARY) , CONTINENT FROM emp_record_table GROUP BY CONTINENT ORDER BY CONTINENT;
