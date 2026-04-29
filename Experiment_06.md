# <center>Experiment No.6
### 1. Display empno, ename, deptno from employee table. Instead of display department numbers display the related department name (Use decode function for ORACLE and CASE for MySQL). 
~~~sql
SELECT 
    EMPNO,
    ENAME,
    CASE DEPTNO
        WHEN 10 THEN 'RESEARCH'
        WHEN 20 THEN 'ACCOUNTING'
        WHEN 30 THEN 'SALES'
        WHEN 40 THEN 'OPERATIONS'
    END AS DNAME
FROM EMPLOYEE;
~~~
### 2. Display your age in days. 
~~~sql
SELECT DATEDIFF(CURDATE(), '2000-01-01') 
AS AGE_IN_DAYS;
~~~
### 3. Display your age in months. 
~~~sql
SELECT TIMESTAMPDIFF(MONTH, '2000-01-01', CURDATE()) 
AS AGE_IN_MONTHS;
~~~
### 4. Display the current date as 15th August Friday Nineteen Ninety-Seven. 
~~~sql
SELECT DATE_FORMAT(CURDATE(), '%D %M %W %Y') 
AS CURRENT_DATE;
~~~
### 5. Display the following output for each row from employee table. 
#### Scott has joined the company on Wednesday 13th August Nineteen Ninety.
~~~sql
SELECT 
CONCAT(
    ENAME,
    ' has joined the company on ',
    DATE_FORMAT(HIREDATE, '%W %D %M %Y')
) AS DETAILS
FROM EMPLOYEE
WHERE ENAME = 'SCOTT';
~~~
### 7. Find the date for nearest Saturday after current date.
~~~sql
SELECT DATE_ADD(
    '2026-02-22',
    INTERVAL MOD(5 - WEEKDAY('2026-02-22') +7, 7) DAY
) AS NEXT_SATURDAY;
~~~
~~~sql
SELECT DATE_ADD(
    '2026-02-22',
    INTERVAL MOD(7 - DAYOFWEEK('2026-02-22') +7, 7) DAY
) AS NEXT_SATURDAY;
~~~
~~~sql
SELECT DATE_ADD(
    CURDATE(),
    INTERVAL (5 - WEEKDAY(CURDATE())) DAY
) AS NEXT_SATURDAY;
~~~
##### Note: The above code is correct for days less than saturday, but when value become negative, then it dosen't work.
### 8. Display current time. 
~~~sql
SELECT CURTIME() AS CURRENT_TIME;
~~~
### 9. Display the date three months Before the current date.
~~~sql
SELECT DATE_SUB(CURDATE(), INTERVAL 3 MONTH) 
AS DATE_BEFORE_3_MONTHS;
~~~
### 10. Display those employees who joined in the company in the month of Dec. 
~~~sql 
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE MONTH(HIREDATE) = 12;
~~~
### 11. Display those employees whose first 2 characters from hire date -last 2 characters of salary. 
~~~sql
SELECT ENAME, HIREDATE, SAL
FROM EMPLOYEE
WHERE LEFT(DATE_FORMAT(HIREDATE,'%y'),2) = RIGHT(SAL,2);
~~~
### 12. Display those employees whose 10% of salary is equal to the year of joining. 
~~~sql
SELECT ENAME, SAL, HIREDATE
FROM EMPLOYEE
WHERE (SAL * 0.10) = YEAR(HIREDATE);
~~~
### 13. Display those employees who joined the company before 15 of the months. 
~~~sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
~~~
### 14. Display those employees who has joined AFTER 15th of the month 
~~~sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DAY(HIREDATE) > 15;
~~~
### 15. Display those employees whose joining DATE is available in deptno.
~~~sql
SELECT ENAME, HIREDATE, DEPTNO
FROM EMPLOYEE
WHERE HIREDATE IS NOT NULL
AND DEPTNO IS NOT NULL;
~~~
    Example (Add 7 days):
    DATE_ADD(date, INTERVAL value interval_type)
    SELECT DATE_ADD('2025-01-01', INTERVAL 7 DAY);
    
    Example (Subtract 3 hours):
    DATE_SUB(date, INTERVAL value interval_type)
    SELECT DATE_SUB('2025-01-01 12:00:00', INTERVAL 3 HOUR);
