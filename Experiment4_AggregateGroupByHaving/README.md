# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many medical records does each doctor have?

Sample table:MedicalRecords Table
For example:

Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3

```sql
select DoctorID ,count(DoctorID) as   TotalRecords
from MedicalRecords
group by DoctorID;
```

**Output:**

<img width="650" height="472" alt="image" src="https://github.com/user-attachments/assets/f6c174ef-2a3f-4542-b673-8703f1cfce48" />

**Question 2**
---
```
How many medical records were created in each month?

Sample table:MedicalRecords Table


For example:

Result
Month       TotalRecords
----------  ------------
2023-12     2
2024-01     6
2024-02     2

```
```sql
SELECT strftime('%Y-%m', date) AS Month,COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY Month
ORDER BY Month;
```

**Output:**

<img width="517" height="311" alt="image" src="https://github.com/user-attachments/assets/d62785db-edf6-4c52-bb24-55ce6ca50a04" />

**Question 3**
---
```
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table

For example:

Result
Medication     AvgDosage
-------------  ----------
Ciprofloxacin  500.0
Doxorubicin    60.0
Ibuprofen      400.0
Levothyroxine  50.0
Lisinopril     10.0
MMR            0.5
Pending        0.0
Prenatal vita  1.0
Sertraline     50.0
Topiramate     25.0

```
```sql
select Medication,avg(Dosage) as AvgDosage from prescriptions group by Medication;
```

**Output:**

<img width="609" height="568" alt="image" src="https://github.com/user-attachments/assets/2f17c994-204c-4d64-b254-8e394ca026da" />

**Question 4**
---
```
Write a SQL query to find  how many employees work in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
employees_in_california
-----------------------
2

```
```sql
select count(id) as employees_in_california
from employee
where city like '%California%';
```

**Output:**

<img width="481" height="228" alt="image" src="https://github.com/user-attachments/assets/bdf9518b-8e88-4610-994c-369bf7201baa" />

**Question 5**
---
```
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8
```
```sql
SELECT COUNT(customer_id) AS "COUNT"
FROM customer;
```

**Output:**

<img width="404" height="242" alt="image" src="https://github.com/user-attachments/assets/7bb14191-33fd-4f92-9651-18a914578f09" />

**Question 6**
---
```
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
AVERAGE
----------
1461.765
```
```sql
SELECT
    AVG(purch_amt) AS AVERAGE
FROM
    orders;
```

**Output:**

<img width="416" height="224" alt="image" src="https://github.com/user-attachments/assets/adf855a5-d5fc-4ae7-8b32-46cb0f2bb3ff" />

**Question 7**
---
```
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
Employee_Name  Age
-------------  ----------
Peter          32
```
```sql
select name as Employee_Name,
min(age) as Age
from employee;
```

**Output:**

<img width="608" height="215" alt="image" src="https://github.com/user-attachments/assets/715e42ce-6dbf-44df-b51f-3be975252488" />

**Question 8**
---
```
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1



For example:

Result
occupation  AVG(workhour)
----------  -------------
Business    10.0
Engineer    12.0
```
```sql
SELECT occupation,AVG(workhour)
FROM employee1
GROUP BY occupation 
HAVING AVG(workhour) BETWEEN 10 AND 12;
```

**Output:**


<img width="514" height="281" alt="image" src="https://github.com/user-attachments/assets/c0bf046f-da16-4a10-b519-0dfa624da723" />

**Question 9**
---
```
Write the SQL query that achieves the grouping of data by city, calculates the average income for each city, and includes only those cities where the average income is greater than 500,000.

Sample table: employee



For example:

Result
city        AVG(income)
----------  -----------
Arizona     1000000.0
California  2650000.0
Florida     2675000.0

```
```sql
SELECT city,AVG(income)
FROM employee
GROUP BY city
HAVING AVG(income) > 500000;
```

**Output:**

<img width="472" height="320" alt="image" src="https://github.com/user-attachments/assets/65387eaa-e2ff-4751-8a10-b4d9edb36cc1" />

**Question 10**
---
```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the maximum work hours for each date, and excludes dates where the maximum work hour is not greater than 12.

Sample table: employee1



For example:

Result
jdate       MAX(workhour)
----------  -------------
2004.0      15
2006.0      15
```
```sql
select jdate,MAX(workhour) from employee1 group by jdate having MAX(workhour)>12;
```

**Output:**


<img width="594" height="295" alt="image" src="https://github.com/user-attachments/assets/c30e9a32-31ea-41f5-ac61-c62c679973d1" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
