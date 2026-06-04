# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616


```sql
INSERT INTO Customers (CustomerID, Name, Address, City, Zipcode)
VALUES (301, 'Michael Jordan', '123 Maple St', 'Chicago', 60616);
```

**Output:**

<img width="1229" height="328" alt="image" src="https://github.com/user-attachments/assets/a08ab634-8a17-425d-bfca-24a85b6e2edf" />


**Question 2**
---
 Write a SQL query to Add a new column State as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           State       TEXT        0                       0


```sql
-- ALTER TABLE Student_details
ADD COLUMN State TEXT;
```

**Output:**

<img width="1238" height="450" alt="image" src="https://github.com/user-attachments/assets/a5064f37-9613-4534-86a3-5ac1f8fe8108" />


**Question 3**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint failed



```sql
-- CREATE TABLE Shipments (
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER REFERENCES Suppliers(SupplierID),
    OrderID INTEGER REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1221" height="322" alt="image" src="https://github.com/user-attachments/assets/ec8fe521-6f59-4427-8615-aa35bcb8425c" />


**Question 4**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL
For example:

Test	Result
INSERT INTO orders (ord_id, item_id, ord_date, ord_qty, cost) VALUES ('O001', 'I001', '2023-08-01', 10, 100);
SELECT * FROM orders;
ord_id      item_id     ord_date    ord_qty     cost
----------  ----------  ----------  ----------  ----------
O001        I001        2023-08-01     10         100

```sql
-- CREATE TABLE orders (
    ord_id TEXT NOT NULL CHECK (LENGTH(ord_id) = 4),
    item_id TEXT NOT NULL,
    ord_date DATE,
    ord_qty INTEGERS,
    cost INTEGER,
    PRIMARY KEY (item_id, ord_date)
);
```

**Output:**

<img width="1199" height="403" alt="image" src="https://github.com/user-attachments/assets/e87b24af-76f4-49c9-8e7e-629cb4360f48" />


**Question 5**
---In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

Test	Result
select * from Student_details;
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science

```sql
-- INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (205, 'Olivia Green', 'F', NULL, NULL);
INSERT INTO Student_details (RollNO, Name, Gender, Subject, MARKS)
VALUES (207, 'Liam Smith', 'M', 'Mathematic', 85);
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (208, 'Sophia Johnson', 'F', 'Science', NULL);
```

**Output:**

<img width="1214" height="375" alt="image" src="https://github.com/user-attachments/assets/350f12e8-6565-4560-8011-ed9b47f41fb1" />


**Question 6**
---
 Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE
For example:

Test	Result
pragma table_info('Events');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EventID     INTEGER     0                       0
1           EventName   TEXT        0                       0
2           EventDate   DATE        0                       0


```sql
-- CREATE TABLE Events (
    EventID INTEGER,
    EventName TEXT,
    EventDate DATE
);
```

**Output:**

<img width="1229" height="461" alt="image" src="https://github.com/user-attachments/assets/491d9661-0718-4601-8839-28259c7247be" />


**Question 7**
---Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78

```sql
-- INSERT INTO student_details
SELECT * FROM Archived_students;
```

**Output:**

<img width="1222" height="377" alt="image" src="https://github.com/user-attachments/assets/11b2d81d-35ce-4f50-b649-6c962093dda2" />


**Question 8**
---
 Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           location     varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0

```sql
-- ALTER TABLE customer
RENAME COLUMN city TO location;
```

**Output:**

<img width="1222" height="435" alt="image" src="https://github.com/user-attachments/assets/5c43f47d-de8d-48ec-b5a3-0c0d33ba74fc" />


**Question 9**
---
 Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000

```sql
-- INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
From Former_employees;
```

**Output:**

<img width="1235" height="350" alt="image" src="https://github.com/user-attachments/assets/32835658-d94d-4186-8b2f-00f43adb0fca" />


**Question 10**
---
 Write a SQL Query  to add attribute Date_of_joining as Date and rename the attribute job_title as Designation in the table 'Employees'

For example:

Test	Result
pragma table_info('Employees');
cid         name         type        notnull     dflt_value  pk
----------  -----------  ----------  ----------  ----------  ----------
0           employee_id  INT         0                       1
1           first_name   VARCHAR(50  0                       0
2           last_name    VARCHAR(50  0                       0
3           Designation  VARCHAR(10  0                       0
4           Date_of_joi  Date        0                       0

```sql
-- ALTER TABLE Employees ADD Date_of_joining Date;
ALTER TABLE Employees RENAME COLUMN job_title TO Designation;
```

**Output:**

<img width="1213" height="425" alt="image" src="https://github.com/user-attachments/assets/2048d8bb-68dd-4a59-ac04-6dd3bbb552aa" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
