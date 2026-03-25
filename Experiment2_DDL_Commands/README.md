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
Create a new table named item with the following specifications and constraints: item_id as TEXT and as primary key. item_desc as TEXT. rate as INTEGER. icom_id as TEXT with a length of 4. icom_id is a foreign key referencing com_id in the company table. The foreign key should set NULL on updates and deletes. item_desc and rate should not accept NULL.

```sql
CREATE TABLE item(
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK(LENGTH(icom_id)=4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
    ON DELETE SET NULL 
    ON UPDATE SET NULL
);
```

**Output:**

<img width="815" height="232" alt="image" src="https://github.com/user-attachments/assets/bd407436-92e9-4dab-8daf-82cc237de267" />


**Question 2**
---
Insert all products from Discontinued_products into Products. Table attributes are ProductID, ProductName, Price, Stock

```sql
insert into Products(ProductID, ProductName, Price, Stock)
SELECT * FROM Discontinued_products; 
```

**Output:**

<img width="812" height="183" alt="image" src="https://github.com/user-attachments/assets/6f22b9db-41a9-40b4-bf97-e7862b99cc8f" />


**Question 3**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key. FirstName and LastName should be NOT NULL. Email should be unique. Salary should be greater than 0. DepartmentID should be a foreign key referencing the Departments table.

```sql
create table Employees(
EmployeeID int primary key,
FirstName text not null,
LastName text not null,
Salary int check(salary>0),
Email text unique,
DepartmentID int,
foreign key (DepartmentID) references Departments(DepartmentID)
);
```

**Output:**

<img width="818" height="345" alt="image" src="https://github.com/user-attachments/assets/8494aaa2-1402-40fc-a6b6-278b060838f4" />


**Question 4**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table

```sql
insert into Student_details(RollNo,Name,Gender,Subject,MARKS)values(201,'David Lee','M','Physics',92)
```

**Output:**

<img width="818" height="157" alt="image" src="https://github.com/user-attachments/assets/e06ae3b2-15bd-4351-b680-564b548706f9" />


**Question 5**
---
Create a table named Members with the following columns:

MemberID as INTEGER MemberName as TEXT JoinDate as DATE

```sql
create table Members(
MemberID INTEGER,
MemberName TEXT,
JoinDate DATE);
```

**Output:**

<img width="817" height="252" alt="image" src="https://github.com/user-attachments/assets/2137b60e-5c08-406c-be26-d165792ae32b" />


**Question 6**
---
Write an SQL query to change the name of the column id to employee_id in the table employee.

```sql
alter table employee  rename id to employee_id; 
```

**Output:**

<img width="821" height="175" alt="image" src="https://github.com/user-attachments/assets/e303a7e3-87d6-4d43-9c91-e93a0fc3587e" />


**Question 7**
---
Create a table named Attendance with the following constraints: AttendanceID as INTEGER should be the primary key. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID). AttendanceDate as DATE. Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
create table Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT ,
    foreign key (EmployeeID) references  Employees(EmployeeID),
    CHECK(Status IN ('Present','Absent','Leave'))
);
```

**Output:**

<img width="817" height="182" alt="image" src="https://github.com/user-attachments/assets/445c089d-93c1-48c3-b068-ce8542dcdabe" />


**Question 8**
---
Insert the following products into the Products table:

Name        Category     Price       Stock<br/>
----------  -----------  ----------  ----------<br/>
Smartphone  Electronics  800         150<br/>
Headphones  Accessories  200         300<br/>

```sql
insert into Products(Name,Category,Price,Stock)values('Smartphone','Electronics',800,150),('Headphones','Accessories',200,300);
```

**Output:**

<img width="815" height="236" alt="image" src="https://github.com/user-attachments/assets/3266002e-d7e0-40e3-a117-c3cf22c37427" />


**Question 9**
---
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id <br/>
-------------+----------------+------------+-------+-------------<br/>
        3002 | Nick Rimando   | New York   |   100 |        5001<br/>
        3007 | Brad Davis     | New York   |   200 |        5001<br/>
        3005 | Graham Zusi    | California |   200 |        5002<br/>

```sql
alter table customer add birth_date timestamp;
```

**Output:**

<img width="817" height="243" alt="image" src="https://github.com/user-attachments/assets/e88e5198-c3f2-4b1e-83e9-2e5b26bec58e" />


**Question 10**
---
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk <br/>
---------------  ---------------  -----  ----------  ----------  ----------<br/>
0                RollNo           int    0                       1<br/>
1                Name             VARCH  1                       0<br/>
2                Gender           TEXT   1                       0<br/>
3                Subject          VARCH  0                       0<br/>
4                MARKS            INT (  0                       0<br/>

```sql

alter table Student_details add Country TEXT;
```

**Output:**

<img width="821" height="232" alt="image" src="https://github.com/user-attachments/assets/229a8861-8216-4a36-911a-5c6003e8b2f6" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
