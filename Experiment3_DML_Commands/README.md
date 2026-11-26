# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
```
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.
```

```sql
UPDATE purchases 
SET per_unit_price = 25,
total_price = quantity * 25
WHERE purchase_date = '2022-08-15'
AND product_id =12;

```

**Output:**

<img width="1352" height="258" alt="image" src="https://github.com/user-attachments/assets/741ec64d-5b35-43dc-86b4-979974a4d900" />

**Question 2**
---
```
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id
```
```sql
UPDATE products SET sell_price=sell_price*1.10 WHERE category='Bakery';
```

**Output:**

<img width="1351" height="253" alt="image" src="https://github.com/user-attachments/assets/145fb0b8-4363-4a49-a24d-ff5cedf367d7" />

**Question 3**
---
```
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE department_id = 20;
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
201          Michael     MHARTSTE    26000       MK_MAN
202          Pat         PFAY        6000        MK_REP


```
```sql
UPDATE Employees
set salary=salary*2
where department_id=20
and job_id like '%MAN';
```

**Output:**

<img width="970" height="158" alt="image" src="https://github.com/user-attachments/assets/1945f233-e278-4b14-86a3-68026164d44e" />

**Question 4**
---
```
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability
```
```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```

**Output:**

<img width="649" height="106" alt="image" src="https://github.com/user-attachments/assets/5ac692b1-a8c5-441f-9d1a-451dd0d2ad27" />

**Question 5**
---
```
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
```
```sql
UPDATE products
SET reorder_lvl = 20
WHERE quantity < 10
AND category = 'Snacks';
```

**Output:**

<img width="1203" height="281" alt="image" src="https://github.com/user-attachments/assets/df9bc2be-f0f9-458a-b5bf-e8b2b69be1f2" />

**Question 6**
---
```
Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```
```sql
DELETE FROM doctors WHERE specialization = 'Cardiology';
```

**Output:**

<img width="691" height="125" alt="image" src="https://github.com/user-attachments/assets/c8df8b94-8394-4d5c-8dc8-2cc62e456451" />

**Question 7**
---
```
Write a SQL query to Select all patients who were admitted during the year 2023.

Table: Patients

name                  type
--------------------  ----------
patient_id            INT
first_name            VARCHAR(50)
last_name             VARCHAR(50)
date_of_birth         DATE
admission_date        DATE
discharge_date        DATE
doctor_id             INT
For example:

Result
patient_id  first_name  admission_date
----------  ----------  --------------
4           Abhishek    2023-02-10
5           Alice       2023-08-02
```
```sql
SELECT patient_id, first_name, admission_date
From Patients
WHERE admission_date BETWEEN '2023-01-01' AND '2023-12-31'
```

**Output:**

<img width="466" height="164" alt="image" src="https://github.com/user-attachments/assets/1fc6d931-f8af-4b85-8cd9-d42a317ae574" />

**Question 8**
---
```
Write a query to get information of Employees from EmployeeInfo1 table where the Employee is not assigned to any department.

EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F
For example:

Result
EmpID       EmpFname    EmpLname    Department  Project     Address         DOB         Gender
----------  ----------  ----------  ----------  ----------  --------------  ----------  ----------
6           Vijay       Mehra                   P1          Hyderabad(HYD)  1976-12-01  M

```
```sql
SELECT *
FROM EmployeeInfo1
WHERE Department is NULL;
```

**Output:**

<img width="972" height="105" alt="image" src="https://github.com/user-attachments/assets/07988954-6c62-4310-9d59-80d39eb6d9f9" />

**Question 9**
---
```
Write a SQL query to Retrieve the department name and location concatenated with a comma

Table name: dept
 
name        type
----------  ----------
deptno       INT
dname       VARCHAR(100)
loc         VARCHAR(100)
For example:

Result
dept_location
-----------------------------------
ACCOUNTING, NEW YORK
RESEARCH, DALLAS
SALES, CHICAGO
OPERATIONS, BOSTON
```
```sql
SELECT dname || ', ' || loc AS dept_location
FROM dept;
```

**Output:**

<img width="450" height="251" alt="image" src="https://github.com/user-attachments/assets/c2f49d92-9bfb-4959-af42-d0b8f75a5c77" />

**Question 10**
---
```
Write a SQL query to find all employees who were hired on a weekend (Saturday or Sunday) from the emp table

emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
For example:

Result
ename       hiredate    day_of_week
----------  ----------  -----------
SMITH       2024-06-02  0
WARD        1981-02-22  0
MILLER      1982-01-23  6
```
```sql
SELECT ename, hiredate, CAST(strftime('%w', hiredate) AS INTEGER) AS day_of_week
From emp
WHERE strftime('%w', hiredate) IN ('0', '6');
```

**Output:**

<img width="457" height="146" alt="image" src="https://github.com/user-attachments/assets/7c7f6958-afc3-47da-b73e-ba818193d281" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
