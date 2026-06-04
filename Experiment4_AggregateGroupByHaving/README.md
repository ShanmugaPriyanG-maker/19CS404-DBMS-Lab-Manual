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
-- How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table



For example:

Result
Specialty          Gender    TotalDoctors
-----------------  --------  --------------
Cardiology         Male      1
Dermatology        Male      1
Gastroenterology   Female    4
Gastroenterology   Male      1
Pediatrics         Female    1
Pediatrics         Male      2

```sql
-- SELECT Specialty, Gender, COUNT(*) AS TotalDoctors
FROM Doctors
GROUP BY Specialty, Gender
ORDER BY Specialty, Gender;
```

**Output:**

<img width="1788" height="1197" alt="image" src="https://github.com/user-attachments/assets/9760a650-c61d-4f3a-aa87-c603fbcc63c1" />


**Question 2**
---
-- What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1


```sql
-- SELECT DoctorID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID
ORDER BY DoctorID;
```

**Output:**

<img width="1789" height="1147" alt="image" src="https://github.com/user-attachments/assets/5293965d-6ab4-4d3a-8d51-c0eee8f35f00" />


**Question 3**
---
-- How many appointments are scheduled for each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
3           3
4           2
6           1
7           3
10          1


```sql
-- SELECT DoctorID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```

**Output:**

<img width="1787" height="1146" alt="image" src="https://github.com/user-attachments/assets/f651b0fd-11a4-48f8-afb7-3939f93320a8" />


**Question 4**
---
-- Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

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


```sql
-- SELECT AVG(purch_amt) AS AVERAGE
FROM orders;
```

**Output:**

<img width="863" height="646" alt="image" src="https://github.com/user-attachments/assets/1bec13a3-d52a-4e7c-87dc-c0f9e1131f5d" />


**Question 5**
---
-- Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4


```sql
-- SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**

<img width="802" height="641" alt="image" src="https://github.com/user-attachments/assets/6934f115-292a-4feb-8da8-6ddbb93caed1" />


**Question 6**
---
-- Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
total
----------
225


```sql
-- SELECT SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

<img width="862" height="636" alt="image" src="https://github.com/user-attachments/assets/679be120-798a-4b67-a2f6-543c304156be" />


**Question 7**
---
-- Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer



 

For example:

Result
COUNT
----------
1


```sql
-- SELECT COUNT(*) AS COUNT
FROM customer
WHERE city = 'Noida';
```

**Output:**

<img width="753" height="634" alt="image" src="https://github.com/user-attachments/assets/75bc4beb-8965-4d02-8883-14387febaccc" />


**Question 8**
---
-- Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

Sample table: products



For example:

Result
category_id  AVG(Price)
-----------  ----------
1            12.375


```sql
-- SELECT category_id, AVG(Price) 
FROM products
GROUP BY category_id
HAVING AVG(price) BETWEEN 10 AND 15;
```

**Output:**

<img width="1019" height="679" alt="image" src="https://github.com/user-attachments/assets/573d3f82-11f1-4be1-8e51-44e90ed2ecc6" />


**Question 9**
---
-- Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1



For example:

Result
occupation  AVG(workhour)
----------  -------------
Business    10.0
Engineer    12.0


```sql
-- SELECT occupation, AVG(workhour)
FROM employee1
GROUP BY occupation
HAVING AVG(workhour) BETWEEN 10 AND 12;
```

**Output:**

<img width="1120" height="760" alt="image" src="https://github.com/user-attachments/assets/a28f3d1a-adf4-40cc-84bd-e3fcdba66f00" />


**Question 10**
---
-- Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee



For example:

Result
city        Income
----------  ----------
Alaska      450000
Arizona     1000000
California  5300000
Florida     5350000
Georgia     250000


```sql
-- SELECT city, SUM(income) AS Income
FROM employee
GROUP BY city
HAVING SUM(income) > 200000;
```

**Output:

<img width="998" height="949" alt="image" src="https://github.com/user-attachments/assets/c0dc7a77-b218-44e6-b0be-5606a9e17e0b" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
