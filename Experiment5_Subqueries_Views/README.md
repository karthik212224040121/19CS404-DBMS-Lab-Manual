# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--

```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500
```

```sql

SELECT *
FROM CUSTOMERS
WHERE SALARY = 1500;
```

**Output:**

<img width="934" height="239" alt="image" src="https://github.com/user-attachments/assets/ff55e076-fd2d-42e8-ba06-f35f79f5dda6" />

**Question 2**
---
```
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70003       2480.4      2012-10-10  3009         5003
70013       3045.6      2012-04-25  3002         5001
```
```sql
select * from orders where purch_amt > (select avg(purch_amt) from orders where ord_date = '2012-10-10');
```

**Output:**

<img width="990" height="341" alt="image" src="https://github.com/user-attachments/assets/2d0768fa-c63e-4550-9c2f-8a8964166114" />

**Question 3**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000
```
```sql
select * from customers where salary<2500;
```

**Output:**

<img width="932" height="334" alt="image" src="https://github.com/user-attachments/assets/a2d0349c-d5b1-4f15-a424-10fa96e9dc46" />

**Question 4**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
3           Kaushik     23          Kota        2000
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
6           Komal       22          Hyderabad   4500
7           Muffy       24          Indore      10000
```
```sql
SELECT * 
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**

<img width="943" height="452" alt="image" src="https://github.com/user-attachments/assets/e7ef952b-ae19-4c89-923c-8ffd2516a1a8" />

**Question 5**
---
```
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
grade       COUNT(*)
----------  ----------
300         2

```
```sql
SELECT grade, COUNT(*) 
FROM customer
WHERE grade > (
SELECT AVG(grade) 
    FROM customer 
    WHERE city = 'New York')
GROUP BY grade;
```

**Output:**

<img width="422" height="235" alt="image" src="https://github.com/user-attachments/assets/2e07ba78-b063-469d-8eb1-b1717097bd11" />

**Question 6**
---
```
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70011       75.29       2012-08-17  3003         5007


```
```sql
SELECT*
FROM Orders
WHERE salesman_id=(SELECT salesman_id FROM Salesman WHERE NAME='Paul Adam');
```

**Output:**

<img width="972" height="281" alt="image" src="https://github.com/user-attachments/assets/f9095368-c187-4ab9-a7f8-abef74222d31" />

**Question 7**
---
```
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
commission
----------
0.14

```
```sql
SELECT commission
FROM salesman
WHERE salesman_id IN(SELECT salesman_id 
     FROM customer
     WHERE city = 'Paris');
```

**Output:**

<img width="262" height="245" alt="image" src="https://github.com/user-attachments/assets/3dc2a83e-ccf6-406e-86fb-f915bf0a3d4a" />

**Question 8**
---
```
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table

name                 type
---------------   ---------------
salesman_id       numeric(5)
name                  varchar(30)
city                     varchar(15)
commission       decimal(5,2)

customer table

name              type
-----------       ----------
customer_id   int
cust_name     text
city                text
grade            int
salesman_id  int

For example:

Result
salesman_id  name
-----------  ----------
5001         James Hoog
5002         Nail Knite

```
```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(*) > 1;
```

**Output:**

<img width="442" height="349" alt="image" src="https://github.com/user-attachments/assets/6d9e48e2-1f70-4e78-b11b-441b4c9360fe" />

**Question 9**
---
```
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
104    Obama            35               Florida          5000000
105    Linklon          32               Georgia          250000
107    Adam             35               California       5000000

```
```sql
SELECT *
FROM Employee
WHERE age < (
 SELECT AVG(age)
 FROM Employee
WHERE income > 250000
);
```

**Output:**

<img width="979" height="319" alt="image" src="https://github.com/user-attachments/assets/5a99060b-c196-4202-b41d-be6cde31749d" />

**Question 10**
---
```
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
For example:

Result
student_name     grade
---------------  ---------------
Charlie          95
Emma             92
John             85
```
```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
SELECT MAX(grade)
 FROM GRADES
WHERE subject = g.subject
);
```

**Output:**

<img width="513" height="257" alt="image" src="https://github.com/user-attachments/assets/3d5e9764-0861-4c0d-b924-36fbf94d8a7b" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
