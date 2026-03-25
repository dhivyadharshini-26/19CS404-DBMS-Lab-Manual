# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.
```
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
```
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```
```
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```


```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name ,
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1324" height="274" alt="438746188-1b61dd39-c786-4872-ade5-2961e66c4443" src="https://github.com/user-attachments/assets/e6960285-061d-4e6b-83bd-506626290321" />


**Question 2**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date,discharge_date, doctor_id

```sql
SELECT p.*
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-01-01' AND '2024-01-31';


```

**Output:**

<img width="1320" height="269" alt="438746827-469801ec-2a5d-4eb8-980f-eb41fe669f1d" src="https://github.com/user-attachments/assets/77e8c1d9-3768-4eef-a626-0c917c1ea83c" />


**Question 3**
---
From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.
```
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
```sql
SELECT c.cust_name AS "Customer Name", 
       c.City AS "city", 
       s.name AS "Salesman", 
       s.commission
FROM customer c
INNER JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;

```

**Output:**


<img width="926" height="513" alt="438747421-d077b5da-28a3-4abb-852b-61dd3e657a43" src="https://github.com/user-attachments/assets/a47b92ec-fdf2-409d-88f4-94eaf3cc3490" />

**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

```sql
SELECT p.first_name AS patient_name, 
       a.*
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id;

```

**Output:**

<img width="1286" height="369" alt="438747824-4333e652-4706-4a94-8247-ac86b49efcd8" src="https://github.com/user-attachments/assets/c3658fe9-5208-4dc4-a8cd-4d96d664d7dc" />


**Question 5**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.
```
PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)
```
```sql
SELECT p.first_name AS patient_name, 
       d.specialization AS Doctor_specialization
FROM patients p
INNER JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="515" height="287" alt="438748166-7465016c-c8b6-410c-a354-1865328ad6fa" src="https://github.com/user-attachments/assets/ef11647a-1a53-4c57-8695-158177d51203" />


**Question 6**
---
From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.
```
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.commission AS "commission"
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id;

```

**Output:**

<img width="917" height="609" alt="438748898-8654eeb2-df95-4379-b49a-10da8d8c9a91" src="https://github.com/user-attachments/assets/5a0bf905-c7ed-4d27-9837-0cdb2c74a388" />


**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date later than '2012-08-17'.
```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';

```

**Output:**

<img width="1052" height="544" alt="438749322-610b79a7-74d7-416e-83cc-603db4074c98" src="https://github.com/user-attachments/assets/2ac8feac-7ede-42c8-91f0-d43aa6544e78" />


**Question 8**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.
```
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.city AS "city",
    s.commission
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
  AND s.commission > 0.12;

```

**Output:**

<img width="1156" height="410" alt="438749851-33acc6f7-f308-453d-b135-49057a85852b" src="https://github.com/user-attachments/assets/6d6be541-efa5-458e-9f28-066c000ff19f" />


**Question 9**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission.
```
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```

```sql
SELECT 
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
JOIN salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1311" height="785" alt="438750476-a74a5321-3891-4378-ae31-5393efe41e20" src="https://github.com/user-attachments/assets/a5796ecb-357b-4f1c-9714-f42da2d881dd" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-07-01' and '2012-07-30'.

```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-07-01' AND '2012-07-30';

```

**Output:**

<img width="1115" height="264" alt="438750943-9e58ff28-8cb5-4728-983b-9f156f9d6879" src="https://github.com/user-attachments/assets/14f57a65-a5a9-4906-af1d-2e1945c150a9" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
