# SQL-ASSIGNMENT-NO-1
Oracle SQL Session - ASSIGNMENT No: 1

						                             	Oracle SQL Session - ASSIGNMENT No: 1
----------------------------------------------------------------------------------------------------------------------------------------
#Creating EMP and DEPT Table:

-Create DEPT table which will be the parent table of the EMP table.

create table dept(   
  deptno     number(2,0),   
  dname      varchar2(14),   
  loc        varchar2(13),   
  constraint pk_dept primary key (deptno)   
)

-Create the EMP table which has a foreign key reference to the DEPT table. The foreign key will require that the DEPTNO in the EMP table exist in the DEPTNO column in the DEPT table.

create table emp(   
  empno    number(4,0),   
  ename    varchar2(10),   
  job      varchar2(9),   
  mgr      number(4,0),   
  hiredate date,   
  sal      number(7,2),   
  comm     number(7,2),   
  deptno   number(2,0),   
  constraint pk_emp primary key (empno),   
  constraint fk_deptno foreign key (deptno) references dept (deptno)   
)

-Insert row into DEPT table using named columns.

insert into DEPT (DEPTNO, DNAME, LOC) 
values(10, 'ACCOUNTING', 'NEW YORK')

insert into dept   
values(20, 'RESEARCH', 'DALLAS')

insert into dept   
values(30, 'SALES', 'CHICAGO')

insert into dept  
values(40, 'OPERATIONS', 'BOSTON')

-Insert EMP row, using TO_DATE function to cast string literal into an oracle DATE format.

insert into emp   
values(   
 7839, 'KING', 'PRESIDENT', null,   
 to_date('17-11-1981','dd-mm-yyyy'),   
 5000, null, 10   
)

insert into emp  
values(  
 7698, 'BLAKE', 'MANAGER', 7839,  
 to_date('1-5-1981','dd-mm-yyyy'),  
 2850, null, 30  
)

insert into emp  
values(  
 7782, 'CLARK', 'MANAGER', 7839,  
 to_date('9-6-1981','dd-mm-yyyy'),  
 2450, null, 10  
)

insert into emp  
values(  
 7566, 'JONES', 'MANAGER', 7839,  
 to_date('2-4-1981','dd-mm-yyyy'),  
 2975, null, 20  
)

insert into emp  
values(  
 7788, 'SCOTT', 'ANALYST', 7566,  
 to_date('13-JUL-87','dd-mm-rr') - 85,  
 3000, null, 20  
)

insert into emp  
values(  
 7902, 'FORD', 'ANALYST', 7566,  
 to_date('3-12-1981','dd-mm-yyyy'),  
 3000, null, 20  
)

insert into emp  
values(  
 7369, 'SMITH', 'CLERK', 7902,  
 to_date('17-12-1980','dd-mm-yyyy'),  
 800, null, 20  
)

insert into emp  
values(  
 7499, 'ALLEN', 'SALESMAN', 7698,  
 to_date('20-2-1981','dd-mm-yyyy'),  
 1600, 300, 30  
)

insert into emp  
values(  
 7521, 'WARD', 'SALESMAN', 7698,  
 to_date('22-2-1981','dd-mm-yyyy'),  
 1250, 500, 30  
)

insert into emp  
values(  
 7654, 'MARTIN', 'SALESMAN', 7698,  
 to_date('28-9-1981','dd-mm-yyyy'),  
 1250, 1400, 30  
)

insert into emp  
values(  
 7844, 'TURNER', 'SALESMAN', 7698,  
 to_date('8-9-1981','dd-mm-yyyy'),  
 1500, 0, 30  
)

insert into emp  
values(  
 7876, 'ADAMS', 'CLERK', 7788,  
 to_date('13-JUL-87', 'dd-mm-rr') - 51,  
 1100, null, 20  
)

insert into emp  
values(  
 7900, 'JAMES', 'CLERK', 7698,  
 to_date('3-12-1981','dd-mm-yyyy'),  
 950, null, 30  
)

insert into emp  
values(  
 7934, 'MILLER', 'CLERK', 7782,  
 to_date('23-1-1982','dd-mm-yyyy'),  
 1300, null, 10  
)

-Simple natural join between DEPT and EMP tables based on the primary key of the DEPT table DEPTNO, and the DEPTNO foreign key in the EMP table.

select ename, dname, job, empno, hiredate, loc   
from emp, dept   
where emp.deptno = dept.deptno   
order by ename

-The GROUP BY clause in the SQL statement allows aggregate functions of non grouped columns. The join is an inner join thus departments with no employees are not displayed.

select dname, count(*) count_of_employees 
from dept, emp 
where dept.deptno = emp.deptno 
group by DNAME 
order by 2 desc

=======================================================================================================================================================================

1.Total Number of Employees.
select count(*) from EMP;

--------------------------------------------------------------------------------------------------------------------

2.Total Number of Departments.
select count(*) from DEPT;

--------------------------------------------------------------------------------------------------------------------

3.All the Employees.
select * from EMP;

--------------------------------------------------------------------------------------------------------------------

4.All the Departments.
select * from DEPT;

--------------------------------------------------------------------------------------------------------------------

5.Total salary paid for all employees.
select * from DEPT;

--------------------------------------------------------------------------------------------------------------------

6.Total commission paid to all employees.
select sum(COMM) from EMP;

--------------------------------------------------------------------------------------------------------------------

7.Which job titles of the employees get commission paid.
select JOB from EMP where COMM>0;

--------------------------------------------------------------------------------------------------------------------

8. System date.
select SYSDATE from dual;

--------------------------------------------------------------------------------------------------------------------

9. Average salary paid to all employees.
select avg(SAL) as average_salary from EMP;

--------------------------------------------------------------------------------------------------------------------

10. How many employees are there in each departments.
select  DEPTNO, count(*) as employee_count from EMP group by DEPTNO;

--------------------------------------------------------------------------------------------------------------------

11. Total salary of the employees in each department.
select DEPTNO, sum(SAL) as TOTAL_DEPT_SALARY from EMP group by DEPTNO;

--------------------------------------------------------------------------------------------------------------------

12. How many employees are there in each departments?
select DEPTNO,count(EMPNO) as TOTAL_EMP from EMP group by DEPTNO;

--------------------------------------------------------------------------------------------------------------------

13. Average salary paid for each job title.
select JOB, AVG(SAL) AS average_salary from EMP group by JOB;

--------------------------------------------------------------------------------------------------------------------

14. Hire day,month and year for each employee.
select  ENAME,to_char(HIREDATE,'day') as HIRE_DAY,to_char(HIREDATE,'month') AS HIRE_MONTH, to_char(HIREDATE,'yyyy') as HIRE_YEAR from EMP ;

--------------------------------------------------------------------------------------------------------------------

15.Sort the Employees department wise
select * from EMP order by DEPTNO;

--------------------------------------------------------------------------------------------------------------------

16. Sort the employees based on their job title.
select * from EMP order by JOB;

--------------------------------------------------------------------------------------------------------------------

17. Sort the employee based on descending order of their salaries;
select * from EMP order by SAL DESC;

--------------------------------------------------------------------------------------------------------------------

18. Sort the employee ascending order of their department and descending order of their salary.
select * from EMP order by  DEPTNO asc , SAL desc;

--------------------------------------------------------------------------------------------------------------------

19.How many employee have their name with 6 characters.
select count(*) from EMP where LENGTH(ENAME) = 6;

--------------------------------------------------------------------------------------------------------------------

20. Maximum and minimum salary paid.
select max(SAL), min(SAL) from EMP;

--------------------------------------------------------------------------------------------------------------------

21.Maximum, minimum, average and sum of salary paid under each department.
select DEPTNO, max(SAL) as MAX_SALARY,min(SAL) as MIN_SALARY,avg(SAL) as AVG_SALARY , sum(SAL) as SUM_SALARY from EMP group by DEPTNO;

--------------------------------------------------------------------------------------------------------------------

22.Sort the employee based on the their hire date
select * from EMP order by HIREDATE;

--------------------------------------------------------------------------------------------------------------------

23.Employee who join latest
select * from EMP order by HIREDATE desc;

--------------------------------------------------------------------------------------------------------------------

24.Who is the oldest employee in the organization based on their hire date.
select * from EMP order by HIREDATE asc;

--------------------------------------------------------------------------------------------------------------------

25.Sort the employee based on their hire year(descending) and department (ascending).
select * from EMP order by to_char(HIREDATE,'yyyy') desc, DEPTNO asc;

--------------------------------------------------------------------------------------------------------------------

26.Employee who get salary greater than or equal to the average salary of employee.
select * from EMP where SAL>=(select avg(SAL) from EMP);

--------------------------------------------------------------------------------------------------------------------

27. Employee who get salary less than or equal to average salary of employee.
select * from EMP where SAL<=(select avg(SAL) from EMP);

--------------------------------------------------------------------------------------------------------------------

28.employee get salary between 2000 and 4000.
select * from EMP where SAL between 2000 and 4000;

--------------------------------------------------------------------------------------------------------------------

29. Which employee get the highest and lowest salary?
select  * from EMP where SAL = (select MAX(SAL) from EMP);
select  * from EMP where SAL = (select MIN(SAL) from EMP);

--------------------------------------------------------------------------------------------------------------------

30.We need to celebrate the joining month of the employees. We plan to buy a gift for each of them. How many gifts do I need to buy for next month?
SELECT COUNT(*) FROM EMP WHERE TO_CHAR(HIREDATE, 'MM') = TO_CHAR(ADD_MONTHS(SYSDATE, 1), 'MM');

----------------------------------------------------------------------------------------------------------------------------------------
										
									                                                 THE END
========================================================================================================================================











































