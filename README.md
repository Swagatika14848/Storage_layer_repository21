# Storage_layer_repository21
https://notepad.pw/StorageLayerAssignment
-- use mysql;
-- create database training21;
use training21;
create table dept(deptno int not null ,dname varchar(20) not null);
drop table dept;
create table dept(
 deptno int not null , 
 dname varchar(20) not null,
 loc varchar(30) not null);
 alter table dept add constraint p_key primary key(deptno);
  INSERT INTO DEPT VALUES (10, 'ACCOUNTING', 'NEW YORK');
 INSERT INTO DEPT VALUES (20, 'RESEARCH',   'DALLAS');
 INSERT INTO DEPT VALUES (30, 'SALES', 'CHICAGO');
 INSERT INTO DEPT VALUES (40, 'OPERATIONS', 'BOSTON');
select * from dept;
show columns in emp;
 CREATE TABLE EMP
(
 EMPNO int NOT NULL,
 ENAME VARCHAR(20),
  JOB VARCHAR(9),
   MGR int ,
    HIREDATE DATETIME,
    SAL NUmeric(7, 2),
    COMM Numeric(7, 2),
    DEPTNO int 
 );
 alter table emp add constraint p_key_empno primary key(empno);
 alter table emp add foreign key (deptno) references dept(deptno);
 -- self foreign key
 alter table emp add constraint f_key foreign key(mgr) references emp(empno);
  INSERT INTO EMP VALUES   (7839, 'KING',   'PRESIDENT', NULL,    str_to_date('11/17/1981','%m/%d/%Y') , 5000, NULL, null);   
INSERT INTO EMP VALUES   (7566, 'JONES',  'MANAGER',   		7839, str_to_date('04/2/1981'	,'%m/%d/%Y'),  2975, NULL, 20);
INSERT INTO EMP VALUES   (7698, 'BLAKE',  'MANAGER',   		7839, str_to_date('05/01/1981'	,'%m/%d/%Y'),  2850, NULL, 30);
INSERT INTO EMP VALUES   (7782, 'CLARK',  'MANAGER',   		7839, str_to_date('06/09/1981'	,'%m/%d/%Y'),  2450, NULL, 10);
INSERT INTO EMP VALUES   (7999, 'RAHUL_DRAVID', 'MANAGER',  7839, str_to_date('01/01/2011'  ,'%m/%d/%Y'), 4000, NULL, 10);
INSERT INTO EMP VALUES   (7788, 'SCOTT',  'ANALYST',   		7566, str_to_date('12/09/1982'  ,'%m/%d/%Y'), 3000, NULL, 20);
INSERT INTO EMP VALUES   (7902, 'FORD',   'ANALYST',   		7566, str_to_date('12/03/1981'  ,'%m/%d/%Y'),  3000, NULL, 20);
INSERT INTO EMP VALUES   (7499, 'ALLEN',  'SALESMAN',  		7698, str_to_date('02/20/1981'  ,'%m/%d/%Y'), 1600,  300, 30);
INSERT INTO EMP VALUES   (7521, 'WARD',   'SALESMAN',  		7698, str_to_date('02/22/1981'  ,'%m/%d/%Y'), 1250,  500, 30);
INSERT INTO EMP VALUES   (7654, 'MARTIN', 'SALESMAN',  		7698, str_to_date('09/28/1981'  ,'%m/%d/%Y'), 1250, 1400, 30);
INSERT INTO EMP VALUES   (7844, 'TURNER', 'SALESMAN',  		7698, str_to_date('09/08/1981'  ,'%m/%d/%Y'),  1500,    0, 30);
INSERT INTO EMP VALUES   (7900, 'JAMES',  'CLERK',			7698, str_to_date('12/03/1981'  ,'%m/%d/%Y'),   950, NULL, 30);
INSERT INTO EMP VALUES   (7369, 'SMITH',  'CLERK',			7902, str_to_date('12/17/1980'  ,'%m/%d/%Y'), 800, NULL, 20);
INSERT INTO EMP VALUES   (7876, 'ADAMS',  'CLERK',			7788, str_to_date('01/12/2003'  ,'%m/%d/%Y'), 1100, NULL, 20);
INSERT INTO EMP VALUES   (7934, 'MILLER', 'CLERK',			7782, str_to_date('01/23/2002'  ,'%m/%d/%Y'), 1300, NULL, 10);
INSERT INTO EMP VALUES   (7901, 'RAHUL_DRAVID', 'MANAGER',  7839, str_to_date('01/23/2012'  ,'%m/%d/%Y'), 3000, NULL, 10);



select * from emp;
-- q1)List all employee manager data
select * from emp where job ='MANAGER';

-- q2)list all employees who are working as manager or analyst or clerk
select * from emp where job in('MANAGER','ANALYST','CLERK');

-- q3)list employees who are getting salary between 3000 to 5000 (inclusive)
select * from emp where sal between 3000 and 5000;

-- q4)List all employees who are getting sal between 3000 and 5000 and job is manager,analyst,or clerk
select * from emp where job in('MANAGER','CLERK','ANALYST') and sal between 3000 and 5000;

-- q5)list employees are are getting comm
select * from emp where comm >0;

-- q6)list all employees whose comm is not null
select * from emp where comm !='null';

-- q7)list all employees who name start with 'S'
select * from emp where ename like 'S%';

-- q8) list all employees whose name end with 'R'
select * from emp where ename like '%R';

-- q9)list all employees whose name contains 'A'
select * from emp where ename like '%A%';

-- q10)list all employees where second letter starts with  alter
select * from emp where ename like '_A%';

-- q11)list all employees whose name start with S or M
select * from emp where ename like 'M%' or ename like 'S%';

show columns in emp;
-- q12)list all employees whose name start between A to M
select * from emp where ename between 'A%' and 'M%';

-- q13)list all employees whose ename contains _
select  * from emp where ename like '%_%'escape '_';

-- q14) list all employees who are working as manager in either dept 10 or 20 and clerk in dept 30
select * from emp where job = 'MANAGER' and deptno in(10,20)  or job='CLERK'  and deptno=30;

-- q15)list ename ,sal and bonus as 10% of salary
select ename ,sal, sal*0.1 as bonus from emp;


select * from emp;
-- q16)list emp data as per ascending order
select * from emp order by ename asc;

-- q17)list all emp as per salary highest to lowest
select * from emp order by sal desc;

-- q18)list emp as per their dept and within dept highest to lowest sal
select * from emp group by deptno order by sal desc;

-- q19)list top 3 highest paid emp
select * from emp order by sal desc limit 0,3;

-- q20) list of sequential number
select ename,deptno ,row_number() over (order by ename desc)as r  from emp ;
-- q21)
select empno,ename,deptno,sal,rank() over(partition by deptno order by sal desc) as 'rank' from emp;
-- q22)list different job name
select distinct(job) from emp;

-- q23)grandtotal of organization salary
select sum(sal) from emp;

-- q24)list deptwize sal 
select sum(sal),deptno from emp group by deptno;

-- q25)list jobwise emp count
select count(job),deptno from emp group by job;

-- q26) list of all emp who are joined in month feb

select * from emp where hiredate like '%02%';

-- q27)list of all emp who are joined between 1981 and 1983
select ename from emp where  year(hiredate) between '1981' and '1983';
use mysql;
use training21;

select * from emp;

-- q29)List of employees based on experienced
select ename,year (now())-year(hiredate) as NoofEx from emp;
