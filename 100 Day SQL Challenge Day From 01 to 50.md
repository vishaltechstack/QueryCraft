# 100-Day SQL Challenge: Day 01 to Day 50

This document contains the first 50 foundational and intermediate SQL practice problems, complete with clean table schemas, sample data, and clear problem statements.

---

### Day 01 – Second Highest Salary
**Table:** `Employees`  
**Columns:** `id`, `name`, `salary`  

Write a query to find the second highest unique salary from the `Employees` table.

```sql
CREATE TABLE Employees (
    id INT,
    name VARCHAR(50),
    salary INT
);

INSERT INTO Employees VALUES
(1, 'A', 50000),
(2, 'B', 60000),
(3, 'C', 70000),
(4, 'D', 70000);
```

---

### Day 02 – Duplicate Emails
**Table:** `Users`  
**Columns:** `id`, `email`  

Write a query to find all duplicate emails in the `Users` table.

```sql
CREATE TABLE Users (
    id INT,
    email VARCHAR(100)
);

INSERT INTO Users VALUES
(1, 'a@gmail.com'),
(2, 'b@gmail.com'),
(3, 'a@gmail.com'),
(4, 'c@gmail.com'),
(5, 'b@gmail.com');
```

---

### Day 03 – Top 3 Salaries (Using Window Functions)
**Table:** `Employees`  
**Columns:** `id`, `name`, `salary`  

Write a query to find the top 3 highest-paid employees using a window function (`DENSE_RANK` or `ROW_NUMBER`).

```sql
CREATE TABLE Employees (
    id INT,
    name VARCHAR(50),
    salary INT
);

INSERT INTO Employees VALUES
(1, 'A', 40000),
(2, 'B', 50000),
(3, 'C', 60000),
(4, 'D', 70000),
(5, 'E', 80000);
```

---

### Day 04 – Employees Earning More Than Their Managers
**Table:** `Employee`  
**Columns:** `id`, `name`, `salary`, `manager_id`  

Write a query to find the names of employees who earn strictly more than their direct managers.

```sql
CREATE TABLE Employee (
    id INT,
    name VARCHAR(50),
    salary INT,
    manager_id INT
);

INSERT INTO Employee VALUES
(1, 'A', 50000, NULL),
(2, 'B', 60000, 1),
(3, 'C', 40000, 1),
(4, 'D', 70000, 2);
```

---

### Day 05 – Customers Who Never Order
**Table:** `Customers`  
**Columns:** `id`, `name`  

**Table:** `Orders`  
**Columns:** `id`, `customer_id`  

Write a query to find all customers who have never placed an order.

```sql
CREATE TABLE Customers (
    id INT,
    name VARCHAR(50)
);

CREATE TABLE Orders (
    id INT,
    customer_id INT
);

INSERT INTO Customers VALUES
(1, 'A'), (2, 'B'), (3, 'C');

INSERT INTO Orders VALUES
(1, 1), (2, 1);
```

---

### Day 06 – Running Total
**Table:** `Sales`  
**Columns:** `id`, `amount`  

Write a query to calculate the cumulative running total of sales ordered by `id`.

```sql
CREATE TABLE Sales (
    id INT,
    amount INT
);

INSERT INTO Sales VALUES
(1, 100),
(2, 200),
(3, 300);
```

---

### Day 07 – Find Nth Highest Salary (3rd Highest)
**Table:** `Employees`  
**Columns:** `id`, `salary`  

Write a query to find the 3rd highest unique salary from the `Employees` table.

```sql
CREATE TABLE Employees (
    id INT,
    salary INT
);

INSERT INTO Employees VALUES
(1, 100),
(2, 200),
(3, 300),
(4, 400);
```

---

### Day 08 – Department Wise Highest Salary
**Table:** `Employee`  
**Columns:** `name`, `salary`, `department`  

Write a query to find the highest salary in each department.

```sql
CREATE TABLE Employee (
    name VARCHAR(50),
    salary INT,
    department VARCHAR(50)
);

INSERT INTO Employee VALUES
('A', 50000, 'IT'),
('B', 60000, 'IT'),
('C', 40000, 'HR'),
('D', 70000, 'HR');
```

---

### Day 09 – Rank Employees by Salary
**Table:** `Employees`  
**Columns:** `name`, `salary`  

Write a query to rank employees from highest to lowest salary without skipping rank numbers when ties occur (`DENSE_RANK`).

```sql
CREATE TABLE Employees (
    name VARCHAR(50),
    salary INT
);

INSERT INTO Employees VALUES
('A', 30000),
('B', 50000),
('C', 50000),
('D', 70000);
```

---

### Day 10 – Find Missing IDs
**Table:** `Numbers`  
**Columns:** `id`  

Write a query to find all missing numbers in the sequence between the minimum and maximum `id` in the `Numbers` table.

```sql
CREATE TABLE Numbers (
    id INT
);

INSERT INTO Numbers VALUES
(1), (2), (4), (6);
```

---

### Day 11 – Total Orders Per Customer
**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`  

Write a query to find the total number of orders placed by each customer.

```sql
CREATE TABLE Orders (
    order_id INT,
    customer_id INT
);

INSERT INTO Orders VALUES
(1, 101),
(2, 101),
(3, 102),
(4, 103),
(5, 101);
```

---

### Day 12 – Customers With More Than 2 Orders
**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`  

Write a query to find all customers who have placed strictly more than 2 orders.

```sql
CREATE TABLE Orders (
    order_id INT,
    customer_id INT
);

INSERT INTO Orders VALUES
(1, 101),
(2, 101),
(3, 102),
(4, 103),
(5, 101);
```

---

### Day 13 – First Order Date for Each Customer
**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`, `order_date`  

Write a query to find the earliest (`first`) order date for each customer.

```sql
CREATE TABLE Orders (
    order_id INT,
    customer_id INT,
    order_date DATE
);

INSERT INTO Orders VALUES
(1, 101, '2023-01-01'),
(2, 101, '2023-02-01'),
(3, 102, '2023-01-15'),
(4, 103, '2023-03-01');
```

---

### Day 14 – Latest Order Per Customer
**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`, `order_date`  

Write a query to retrieve the most recent (`latest`) order record for each customer.

```sql
CREATE TABLE Orders (
    order_id INT,
    customer_id INT,
    order_date DATE
);

INSERT INTO Orders VALUES
(1, 101, '2023-01-01'),
(2, 101, '2023-02-01'),
(3, 102, '2023-01-15'),
(4, 103, '2023-03-01');
```

---

### Day 15 – Pivot Data Using CASE
**Table:** `Sales`  
**Columns:** `product`, `year`, `amount`  

Write a query to pivot the `Sales` table so each product appears once with separate columns for `sales_2022` and `sales_2023`.

```sql
CREATE TABLE Sales (
    product VARCHAR(50),
    year INT,
    amount INT
);

INSERT INTO Sales VALUES
('A', 2022, 100),
('A', 2023, 150),
('B', 2022, 200),
('B', 2023, 250);
```

---

### Day 16 – Find Consecutive Records
**Table:** `Logs`  
**Columns:** `id`, `num`  

Write a query to find all numbers (`num`) that appear at least 2 times consecutively based on `id`.

```sql
CREATE TABLE Logs (
    id INT,
    num INT
);

INSERT INTO Logs VALUES
(1, 1),
(2, 1),
(3, 2),
(4, 3),
(5, 3);
```

---

### Day 17 – CTE Basic Usage
**Table:** `Employees`  
**Columns:** `id`, `salary`  

Write a query using a Common Table Expression (CTE) to find all employees earning strictly above the company's average salary.

```sql
CREATE TABLE Employees (
    id INT,
    salary INT
);

INSERT INTO Employees VALUES
(1, 30000),
(2, 50000),
(3, 70000),
(4, 40000);
```

---

### Day 18 – Percentage Contribution
**Table:** `Employees`  
**Columns:** `name`, `salary`  

Write a query to calculate each employee's percentage contribution to the total company payroll.

```sql
CREATE TABLE Employees (
    name VARCHAR(50),
    salary INT
);

INSERT INTO Employees VALUES
('A', 30000),
('B', 30000),
('C', 40000);
```

---

### Day 19 – Remove Duplicates (Keep One Record)
**Table:** `Users`  
**Columns:** `id`, `email`  

Write a query (or `DELETE` statement) to remove duplicate emails from the `Users` table while keeping only the record with the smallest `id`.

```sql
CREATE TABLE Users (
    id INT,
    email VARCHAR(100)
);

INSERT INTO Users VALUES
(1, 'john@example.com'),
(2, 'bob@example.com'),
(3, 'john@example.com'),
(4, 'alice@example.com'),
(5, 'bob@example.com');
```

---

### Day 20 – Find Median Salary
**Table:** `Employees`  
**Columns:** `salary`  

Write a query to find the median salary from the `Employees` table.

```sql
CREATE TABLE Employees (
    salary INT
);

INSERT INTO Employees VALUES
(100), (200), (300), (400), (500);
```

---

### Day 21 – Second Highest Salary Per Department
**Table:** `Employee`  
**Columns:** `name`, `salary`, `department`  

Write a query to find the second highest salary in each department.

```sql
CREATE TABLE Employee (
    name VARCHAR(50),
    salary INT,
    department VARCHAR(50)
);

INSERT INTO Employee VALUES
('A', 50000, 'IT'),
('B', 60000, 'IT'),
('C', 70000, 'IT'),
('D', 40000, 'HR'),
('E', 30000, 'HR'),
('F', 20000, 'HR');
```

---

### Day 22 – Highest Salary in Each Department (With Employee Name)
**Table:** `Employee`  
**Columns:** `id`, `name`, `salary`, `department`  

Write a query to find the employee(s) who earn the highest salary in each department.

```sql
CREATE TABLE Employee (
    id INT,
    name VARCHAR(50),
    salary INT,
    department VARCHAR(50)
);

INSERT INTO Employee VALUES
(1, 'A', 50000, 'IT'),
(2, 'B', 70000, 'IT'),
(3, 'C', 70000, 'IT'),
(4, 'D', 40000, 'HR'),
(5, 'E', 60000, 'HR');
```

---

### Day 23 – Daily Active Users
**Table:** `Activity`  
**Columns:** `user_id`, `activity_date`  

Write a query to count the number of unique Daily Active Users (DAU) for each `activity_date`.

```sql
CREATE TABLE Activity (
    user_id INT,
    activity_date DATE
);

INSERT INTO Activity VALUES
(1, '2023-01-01'),
(2, '2023-01-01'),
(1, '2023-01-01'),
(1, '2023-01-02'),
(3, '2023-01-02');
```

---

### Day 24 – Rolling 3-Day Sum
**Table:** `Sales`  
**Columns:** `date`, `amount`  

Write a query to calculate the 3-day rolling sum of sales (current day plus the 2 preceding days) ordered by `date`.

```sql
CREATE TABLE Sales (
    date DATE,
    amount INT
);

INSERT INTO Sales VALUES
('2023-01-01', 100),
('2023-01-02', 200),
('2023-01-03', 300),
('2023-01-04', 400);
```

---

### Day 25 – Find Gaps Between Dates
**Table:** `Orders`  
**Columns:** `order_date`  

Write a query to calculate the number of days elapsed between each order date and the immediately preceding order date.

```sql
CREATE TABLE Orders (
    order_date DATE
);

INSERT INTO Orders VALUES
('2023-01-01'),
('2023-01-05'),
('2023-01-10');
```

---

### Day 26 – Identify Returning Customers
**Table:** `Purchases`  
**Columns:** `purchase_id`, `customer_id`, `purchase_date`  

Write a query to find customers who have made more than one purchase on different dates.

```sql
CREATE TABLE Purchases (
    purchase_id INT,
    customer_id INT,
    purchase_date DATE
);

INSERT INTO Purchases VALUES
(1, 101, '2023-01-01'),
(2, 101, '2023-01-15'),
(3, 102, '2023-01-05'),
(4, 103, '2023-01-10'),
(5, 103, '2023-01-10');
```

---

### Day 27 – Top Product by Sales
**Table:** `Sales`  
**Columns:** `product`, `amount`  

Write a query to find the product with the highest total sales amount.

```sql
CREATE TABLE Sales (
    product VARCHAR(50),
    amount INT
);

INSERT INTO Sales VALUES
('A', 100),
('B', 200),
('A', 300),
('B', 100);
```

---

### Day 28 – Monthly Sales Report
**Table:** `Sales`  
**Columns:** `sale_date`, `amount`  

Write a query to calculate the total sales revenue grouped by year and month (`YYYY-MM`).

```sql
CREATE TABLE Sales (
    sale_date DATE,
    amount INT
);

INSERT INTO Sales VALUES
('2023-01-01', 100),
('2023-01-15', 200),
('2023-02-01', 300);
```

---

### Day 29 – Find Customers With No Activity in Last 30 Days
**Table:** `Customers`  
**Columns:** `customer_id`, `customer_name`  

**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`, `order_date`  

Write a query to find customers who have not placed any orders in the last 30 days (assuming today's reference date is `'2023-03-01'`).

```sql
CREATE TABLE Customers (
    customer_id INT,
    customer_name VARCHAR(50)
);

CREATE TABLE Orders (
    order_id INT,
    customer_id INT,
    order_date DATE
);

INSERT INTO Customers VALUES
(101, 'Alice'),
(102, 'Bob'),
(103, 'Charlie');

INSERT INTO Orders VALUES
(1, 101, '2023-02-20'),
(2, 102, '2023-01-10');
```

---

### Day 30 – Session Duration Per User
**Table:** `Sessions`  
**Columns:** `user_id`, `login_time`, `logout_time`  

Write a query to calculate the total session duration (in minutes) for each user.

```sql
CREATE TABLE Sessions (
    user_id INT,
    login_time DATETIME,
    logout_time DATETIME
);

INSERT INTO Sessions VALUES
(1, '2023-01-01 10:00:00', '2023-01-01 11:00:00'),
(2, '2023-01-01 09:00:00', '2023-01-01 10:30:00');
```

---

### Day 31 – Customers With Highest Spend
**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`, `amount`  

Write a query to find the `customer_id` who has spent the highest total amount across all orders.

```sql
CREATE TABLE Orders (
    order_id INT,
    customer_id INT,
    amount INT
);

INSERT INTO Orders VALUES
(1, 101, 500),
(2, 102, 300),
(3, 101, 700),
(4, 103, 400);
```

---

### Day 32 – Find Duplicate Records (Full Row)
**Table:** `Users`  
**Columns:** `id`, `name`, `email`  

Write a query to find exact duplicate rows where all columns (`id`, `name`, `email`) match.

```sql
CREATE TABLE Users (
    id INT,
    name VARCHAR(50),
    email VARCHAR(100)
);

INSERT INTO Users VALUES
(1, 'A', 'a@gmail.com'),
(2, 'B', 'b@gmail.com'),
(1, 'A', 'a@gmail.com');
```

---

### Day 33 – Employees Without Department
**Table:** `Employees`  
**Columns:** `id`, `name`, `dept_id`  

**Table:** `Departments`  
**Columns:** `id`, `dept_name`  

Write a query to find all employees who are not assigned to any valid department.

```sql
CREATE TABLE Employees (
    id INT,
    name VARCHAR(50),
    dept_id INT
);

CREATE TABLE Departments (
    id INT,
    dept_name VARCHAR(50)
);

INSERT INTO Employees VALUES
(1, 'A', 1),
(2, 'B', NULL),
(3, 'C', 2);

INSERT INTO Departments VALUES
(1, 'IT'),
(2, 'HR');
```

---

### Day 34 – Top 2 Products Per Category
**Table:** `Sales`  
**Columns:** `product`, `category`, `amount`  

Write a query to find the top 2 highest-selling products within each `category`.

```sql
CREATE TABLE Sales (
    product VARCHAR(50),
    category VARCHAR(50),
    amount INT
);

INSERT INTO Sales VALUES
('A', 'Electronics', 500),
('B', 'Electronics', 700),
('C', 'Electronics', 600),
('D', 'Clothing', 300),
('E', 'Clothing', 400);
```

---

### Day 35 – Orders Above Average
**Table:** `Orders`  
**Columns:** `order_id`, `amount`  

Write a query to find all orders whose `amount` is strictly greater than the overall average order amount.

```sql
CREATE TABLE Orders (
    order_id INT,
    amount INT
);

INSERT INTO Orders VALUES
(1, 100),
(2, 200),
(3, 300),
(4, 400);
```

---

### Day 36 – Running Difference
**Table:** `Sales`  
**Columns:** `date`, `amount`  

Write a query to calculate the difference in `amount` between the current day and the previous day.

```sql
CREATE TABLE Sales (
    date DATE,
    amount INT
);

INSERT INTO Sales VALUES
('2023-01-01', 100),
('2023-01-02', 150),
('2023-01-03', 200);
```

---

### Day 37 – Detect First Login
**Table:** `Logins`  
**Columns:** `user_id`, `login_date`  

Write a query to find the very first login date for each user.

```sql
CREATE TABLE Logins (
    user_id INT,
    login_date DATE
);

INSERT INTO Logins VALUES
(1, '2023-01-01'),
(1, '2023-01-05'),
(2, '2023-01-03');
```

---

### Day 38 – Consecutive Days Activity
**Table:** `Logins`  
**Columns:** `user_id`, `login_date`  

Write a query to find all users who logged in on at least 2 consecutive calendar days.

```sql
CREATE TABLE Logins (
    user_id INT,
    login_date DATE
);

INSERT INTO Logins VALUES
(1, '2023-01-01'),
(1, '2023-01-02'),
(2, '2023-01-01'),
(2, '2023-01-03');
```

---

### Day 39 – Revenue Growth
**Table:** `Revenue`  
**Columns:** `date`, `amount`  

Write a query to calculate the day-over-day (DoD) percentage revenue growth.

```sql
CREATE TABLE Revenue (
    date DATE,
    amount INT
);

INSERT INTO Revenue VALUES
('2023-01-01', 100),
('2023-01-02', 150),
('2023-01-03', 120);
```

---

### Day 40 – Most Frequent Value
**Table:** `Numbers`  
**Columns:** `num`  

Write a query to find the mode (the most frequently occurring number) in the `Numbers` table.

```sql
CREATE TABLE Numbers (
    num INT
);

INSERT INTO Numbers VALUES
(1), (2), (2), (3), (3), (3);
```

---

### Day 41 – User Retention (Next Day)
**Table:** `Logins`  
**Columns:** `user_id`, `login_date`  

Write a query to calculate the Day 1 to Day 2 retention rate (the fraction/percentage of users who logged back in the day immediately following their first login date).

```sql
CREATE TABLE Logins (
    user_id INT,
    login_date DATE
);

INSERT INTO Logins VALUES
(1, '2023-01-01'),
(1, '2023-01-02'),
(2, '2023-01-01'),
(2, '2023-01-03'),
(3, '2023-01-01'),
(3, '2023-01-02');
```

---

### Day 42 – Funnel Conversion (Visit to Purchase)
**Table:** `Events`  
**Columns:** `user_id`, `event_type`  

Write a query to count how many users completed both a `'visit'` event and a `'purchase'` event.

```sql
CREATE TABLE Events (
    user_id INT,
    event_type VARCHAR(50)
);

INSERT INTO Events VALUES
(1, 'visit'),
(1, 'purchase'),
(2, 'visit'),
(3, 'purchase'),
(4, 'visit'),
(4, 'purchase');
```

---

### Day 43 – Cohort Analysis (Monthly)
**Table:** `Orders`  
**Columns:** `user_id`, `order_date`  

Write a query to assign each user to a monthly cohort based on their first purchase month and count the number of users in each cohort.

```sql
CREATE TABLE Orders (
    user_id INT,
    order_date DATE
);

INSERT INTO Orders VALUES
(1, '2023-01-10'),
(1, '2023-02-10'),
(2, '2023-01-15'),
(3, '2023-02-01');
```

---

### Day 44 – Churned Users
**Table:** `Logins`  
**Columns:** `user_id`, `login_date`  

Write a query to find one-time users who never returned after their initial login date.

```sql
CREATE TABLE Logins (
    user_id INT,
    login_date DATE
);

INSERT INTO Logins VALUES
(1, '2023-01-01'),
(1, '2023-01-02'),
(2, '2023-01-01'),
(3, '2023-01-01'),
(3, '2023-01-05');
```

---

### Day 45 – Average Time Between Orders
**Table:** `Orders`  
**Columns:** `user_id`, `order_date`  

Write a query to calculate the average number of days between consecutive orders for each user.

```sql
CREATE TABLE Orders (
    user_id INT,
    order_date DATE
);

INSERT INTO Orders VALUES
(1, '2023-01-01'),
(1, '2023-01-05'),
(1, '2023-01-10');
```

---

### Day 46 – Peak Usage Day
**Table:** `Logins`  
**Columns:** `login_date`  

Write a query to find the `login_date` with the highest number of logins.

```sql
CREATE TABLE Logins (
    login_date DATE
);

INSERT INTO Logins VALUES
('2023-01-01'),
('2023-01-01'),
('2023-01-02');
```

---

### Day 47 – Revenue Per User
**Table:** `Orders`  
**Columns:** `user_id`, `amount`  

Write a query to calculate the total revenue generated by each user.

```sql
CREATE TABLE Orders (
    user_id INT,
    amount INT
);

INSERT INTO Orders VALUES
(1, 100),
(1, 200),
(2, 300);
```

---

### Day 48 – Identify Power Users
**Table:** `Logins`  
**Columns:** `user_id`  

Write a query to find power users who have logged in 3 or more times.

```sql
CREATE TABLE Logins (
    user_id INT
);

INSERT INTO Logins VALUES
(1),(1),(1),(2),(2),(3);
```

---

### Day 49 – Session Overlap
**Table:** `Sessions`  
**Columns:** `user_id`, `start_time`, `end_time`  

Write a query to detect users who have overlapping concurrent sessions.

```sql
CREATE TABLE Sessions (
    user_id INT,
    start_time DATETIME,
    end_time DATETIME
);

INSERT INTO Sessions VALUES
(1, '2023-01-01 10:00:00', '2023-01-01 11:00:00'),
(1, '2023-01-01 10:30:00', '2023-01-01 11:30:00');
```

---

### Day 50 – Rolling Average (7-Day)
**Table:** `Sales`  
**Columns:** `date`, `amount`  

Write a query to compute the 7-day rolling average of daily sales (current day and up to 6 preceding days).

```sql
CREATE TABLE Sales (
    date DATE,
    amount INT
);

INSERT INTO Sales VALUES
('2023-01-01', 100),
('2023-01-02', 200),
('2023-01-03', 300),
('2023-01-04', 400);
```