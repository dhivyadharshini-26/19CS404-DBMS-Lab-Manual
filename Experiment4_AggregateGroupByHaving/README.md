# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.
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
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table
```
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
SELECT
  Medication,
  AVG(Dosage) AS AvgDosage
FROM
  Prescriptions
GROUP BY
  Medication;

```

**Output:**

<img width="695" height="742" alt="image" src="https://github.com/user-attachments/assets/c347673f-5e6b-4e9d-b49e-196071e39b1d" />


**Question 2**
---
How many patients are there in each city?

Sample table: Patients Table
```
Address     TotalPatients
----------  -------------
Berlin      3
Chicago     4
Mexico      3
```

```sql
select Address,count(*)
as TotalPatients
from Patients
group by Address
```

**Output:**

<img width="658" height="392" alt="image" src="https://github.com/user-attachments/assets/848773cb-0780-4263-aa5e-36616d7f2f90" />


**Question 3**
---
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table
```

PatientID   AvgMedications
----------  --------------
4           5
6           1
7           1
8           3
```

```sql
SELECT PatientID,COUNT(*) AS 
AvgMedications
FROM MedicalRecords
GROUP BY PatientID;
```

**Output:**

<img width="677" height="612" alt="image" src="https://github.com/user-attachments/assets/474f243d-b382-4cbc-8830-747a33d7c330" />


**Question 4**
---
Write a SQL query to find the maximum purchase amount.

Sample table: orders
```
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```

```sql
SELECT
  MAX(purch_amt) AS MAXIMUM
FROM
  orders;
```

**Output:**

<img width="403" height="297" alt="image" src="https://github.com/user-attachments/assets/39fa51d7-2e95-48f2-a7eb-50586ad8eec0" />


**Question 5**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee
```
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```
```sql
SELECT
  SUM(income) AS total_income
FROM
  employee
WHERE
  age >= 40;
```

**Output:**

<img width="437" height="311" alt="image" src="https://github.com/user-attachments/assets/05a9c241-b52b-4c65-873e-b560f079b47a" />


**Question 6**
---
Write a SQL query to find the number of employees whose age is greater than 32.


```sql
SELECT
  COUNT(*) AS COUNT
FROM
  employee
WHERE
  age > 32;
```

**Output:**

<img width="435" height="316" alt="image" src="https://github.com/user-attachments/assets/c93b4873-45af-4fdd-934e-699dd60730de" />

**Question 7**
---
Write a SQL query to find the average length of names for people living in Chennai?

Table: customer
```
name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
```

```sql
SELECT
  AVG(LENGTH(name)) AS avg_name_length
FROM
  customer
WHERE
  city = 'Chennai';
```

**Output:**

<img width="438" height="295" alt="image" src="https://github.com/user-attachments/assets/043bd99b-a9d2-4bba-bb82-76daf0a1684d" />

**Question 8**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the maximum work hours for each date, and excludes dates where the maximum work hour is not greater than 12.

Sample table: employee1
```
jdate       MAX(workhour)
----------  -------------
2004.0      15
2006.0      15
```

```sql
SELECT
  jdate,
  MAX(workhour) AS "MAX(workhour)"
FROM
  employee1
GROUP BY
  jdate
HAVING
  MAX(workhour) > 12;
```

**Output:**

<img width="670" height="377" alt="image" src="https://github.com/user-attachments/assets/d190c7b4-dbda-44de-a3bc-94c9ccdecf51" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1
```
occupation  SUM(workhour)
----------  -------------
Business    30
Doctor      30
Engineer    24
Teacher     27
```

```sql
SELECT
  occupation,
  SUM(workhour) AS "SUM(workhour)"
FROM
  employee1
GROUP BY
  occupation
HAVING
  SUM(workhour) > 20;
```

**Output:**

<img width="616" height="437" alt="image" src="https://github.com/user-attachments/assets/901be72e-8384-4d00-92f0-fc707bfdd8ef" />

**Question 10**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1
```
Result
occupation  AVG(workhour)
----------  -------------
Business    10.0
Engineer    12.0
```

```sql
SELECT
  occupation,
  AVG(workhour) AS "AVG(workhour)"
FROM
  employee1
GROUP BY
  occupation
HAVING
  AVG(workhour) BETWEEN 10 AND 12;
```

**Output:**

<img width="753" height="387" alt="image" src="https://github.com/user-attachments/assets/f8038c39-ebd7-4fbb-84fd-608829951be1" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

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
-- Paste Question 1 here

```sql
-- Paste your SQL code below for Question 1
```

**Output:**

![Output1](output.png)

**Question 2**
---
-- Paste Question 2 here

```sql
-- Paste your SQL code below for Question 2
```

**Output:**

![Output2](output.png)

**Question 3**
---
-- Paste Question 3 here

```sql
-- Paste your SQL code below for Question 3
```

**Output:**

![Output3](output.png)

**Question 4**
---
-- Paste Question 4 here

```sql
-- Paste your SQL code below for Question 4
```

**Output:**

![Output4](output.png)

**Question 5**
---
-- Paste Question 5 here

```sql
-- Paste your SQL code below for Question 5
```

**Output:**

![Output5](output.png)

**Question 6**
---
-- Paste Question 6 here

```sql
-- Paste your SQL code below for Question 6
```

**Output:**

![Output6](output.png)

**Question 7**
---
-- Paste Question 7 here

```sql
-- Paste your SQL code below for Question 7
```

**Output:**

![Output7](output.png)

**Question 8**
---
-- Paste Question 8 here

```sql
-- Paste your SQL code below for Question 8
```

**Output:**

![Output8](output.png)

**Question 9**
---
-- Paste Question 9 here

```sql
-- Paste your SQL code below for Question 9
```

**Output:**

![Output9](output.png)

**Question 10**
---
-- Paste Question 10 here

```sql
-- Paste your SQL code below for Question 10
```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
