# 100-Day SQL Challenge: Day 51 to Day 100

This document contains 50 practice SQL problems spanning advanced SQL topics including Window Functions, CTEs, Data Cleaning, Date/Time Manipulations, Complex Joins, and Analytical Aggregations.

---

### Day 51 – Manager With At Least 5 Direct Reports
**Table:** `Employee`  
**Columns:** `id`, `name`, `department`, `managerId`  

Write a query to find the names of managers who have at least five direct reports.

```sql
CREATE TABLE Employee (
    id INT,
    name VARCHAR(50),
    department VARCHAR(50),
    managerId INT
);

INSERT INTO Employee VALUES
(101, 'John', 'A', NULL),
(102, 'Dan', 'A', 101),
(103, 'James', 'A', 101),
(104, 'Amy', 'A', 101),
(105, 'Anne', 'A', 101),
(106, 'Ron', 'B', 101);
```

---

### Day 52 – Year-over-Year (YoY) Growth Rate
**Table:** `User_Transactions`  
**Columns:** `transaction_id`, `product_id`, `spend`, `transaction_date`  

Write a query to calculate the Year-over-Year (YoY) growth rate for the total spend of each product.

```sql
CREATE TABLE User_Transactions (
    transaction_id INT,
    product_id INT,
    spend DECIMAL(10, 2),
    transaction_date DATE
);

INSERT INTO User_Transactions VALUES
(1341, 123424, 1500.60, '2023-12-31'),
(1423, 123424, 1000.20, '2024-12-31'),
(1623, 123424, 1246.44, '2025-12-31'),
(1322, 123424, 2145.32, '2026-12-31');
```

---

### Day 53 – Mutual Friends Count
**Table:** `Friends`  
**Columns:** `user_id`, `friend_id`  

Write a query to find the number of mutual friends between user `1` and user `2`.

```sql
CREATE TABLE Friends (
    user_id INT,
    friend_id INT
);

INSERT INTO Friends VALUES
(1, 2), (1, 3), (1, 4), (1, 5),
(2, 1), (2, 3), (2, 4), (2, 6);
```

---

### Day 54 – Exchange Seats (Swap Consecutive Students)
**Table:** `Seat`  
**Columns:** `id`, `student`  

Write a query to swap the seat ID of every two consecutive students. If the number of students is odd, the ID of the last student is not swapped.

```sql
CREATE TABLE Seat (
    id INT,
    student VARCHAR(50)
);

INSERT INTO Seat VALUES
(1, 'Abbot'),
(2, 'Doris'),
(3, 'Emerson'),
(4, 'Green'),
(5, 'Jeames');
```

---

### Day 55 – Find Cumulative Percentage (Pareto 80/20 Rule)
**Table:** `Product_Sales`  
**Columns:** `product_name`, `revenue`  

Write a query to calculate the cumulative percentage of total revenue contributed by each product, ordered from highest to lowest revenue.

```sql
CREATE TABLE Product_Sales (
    product_name VARCHAR(50),
    revenue INT
);

INSERT INTO Product_Sales VALUES
('Laptop', 50000),
('Phone', 30000),
('Tablet', 10000),
('Headphones', 6000),
('Charger', 4000);
```

---

### Day 56 – Customers Who Bought All Products
**Table:** `Customer_Purchases`  
**Columns:** `customer_id`, `product_key`  

**Table:** `Products`  
**Columns:** `product_key`  

Write a query to report the customer IDs from the `Customer_Purchases` table that bought all the products listed in the `Products` table.

```sql
CREATE TABLE Products (
    product_key INT
);

INSERT INTO Products VALUES (5), (6);

CREATE TABLE Customer_Purchases (
    customer_id INT,
    product_key INT
);

INSERT INTO Customer_Purchases VALUES
(1, 5),
(2, 6),
(3, 5),
(3, 6),
(1, 6);
```

---

### Day 57 – Find Start and End of Continuous Ranges (Islands Problem)
**Table:** `Logs`  
**Columns:** `log_id`  

Write a query to find the start and end number of continuous ranges in the `Logs` table.

```sql
CREATE TABLE Logs (
    log_id INT
);

INSERT INTO Logs VALUES
(1), (2), (3), (7), (8), (10);
```

---

### Day 58 – Cancellation Rate of Trips
**Table:** `Trips`  
**Columns:** `id`, `client_id`, `driver_id`, `status`, `request_at`  

**Table:** `Users`  
**Columns:** `users_id`, `banned`, `role`  

Write a query to find the cancellation rate of requests with unbanned users (both client and driver must not be banned) each day.

```sql
CREATE TABLE Users (
    users_id INT,
    banned VARCHAR(10),
    role VARCHAR(20)
);

INSERT INTO Users VALUES
(1, 'No', 'client'),
(2, 'Yes', 'client'),
(10, 'No', 'driver');

CREATE TABLE Trips (
    id INT,
    client_id INT,
    driver_id INT,
    status VARCHAR(30),
    request_at DATE
);

INSERT INTO Trips VALUES
(1, 1, 10, 'completed', '2026-10-01'),
(2, 2, 10, 'cancelled_by_driver', '2026-10-01'),
(3, 1, 10, 'cancelled_by_client', '2026-10-02');
```

---

### Day 59 – Recursive Org Chart (Employee Hierarchy Level)
**Table:** `Staff`  
**Columns:** `emp_id`, `emp_name`, `manager_id`  

Write a query using a Recursive CTE to find each employee's hierarchy level (CEO = Level 1, direct reports = Level 2, and so on).

```sql
CREATE TABLE Staff (
    emp_id INT,
    emp_name VARCHAR(50),
    manager_id INT
);

INSERT INTO Staff VALUES
(1, 'Alice (CEO)', NULL),
(2, 'Bob (VP)', 1),
(3, 'Charlie (Manager)', 2),
(4, 'David (Developer)', 3);
```

---

### Day 60 – Market Basket Analysis (Frequently Bought Together)
**Table:** `Order_Items`  
**Columns:** `order_id`, `product_name`  

Write a query to find the top pairs of products that are most frequently bought together in the same order.

```sql
CREATE TABLE Order_Items (
    order_id INT,
    product_name VARCHAR(50)
);

INSERT INTO Order_Items VALUES
(1, 'Bread'), (1, 'Butter'), (1, 'Milk'),
(2, 'Bread'), (2, 'Butter'),
(3, 'Bread'), (3, 'Milk'),
(4, 'Butter'), (4, 'Milk');
```

---

### Day 61 – Department Top Three Salaries (Including Ties)
**Table:** `Employee`  
**Columns:** `id`, `name`, `salary`, `departmentId`  

**Table:** `Department`  
**Columns:** `id`, `name`  

Write a query to find employees who earn one of the top three unique salaries in each of their respective departments.

```sql
CREATE TABLE Department (
    id INT,
    name VARCHAR(50)
);

INSERT INTO Department VALUES
(1, 'IT'),
(2, 'Sales');

CREATE TABLE Employee (
    id INT,
    name VARCHAR(50),
    salary INT,
    departmentId INT
);

INSERT INTO Employee VALUES
(1, 'Joe', 85000, 1),
(2, 'Henry', 80000, 2),
(3, 'Sam', 60000, 2),
(4, 'Max', 90000, 1),
(5, 'Janet', 69000, 1),
(6, 'Randy', 85000, 1),
(7, 'Will', 70000, 1);
```

---

### Day 62 – Consecutive Available Seats in a Cinema
**Table:** `Cinema`  
**Columns:** `seat_id`, `free`  

Write a query to report all the consecutive available (`free = 1`) seats in the cinema, ordered by `seat_id` ascending.

```sql
CREATE TABLE Cinema (
    seat_id INT,
    free INT
);

INSERT INTO Cinema VALUES
(1, 1),
(2, 0),
(3, 1),
(4, 1),
(5, 1),
(6, 0),
(7, 1);
```

---

### Day 63 – Customer Churn & Reactivation (Win-Back Users)
**Table:** `Monthly_Logins`  
**Columns:** `user_id`, `login_month`  

Write a query to identify users who were active in a given month, inactive the very next month, and returned the month after that.

```sql
CREATE TABLE Monthly_Logins (
    user_id INT,
    login_month DATE
);

INSERT INTO Monthly_Logins VALUES
(101, '2026-01-01'),
(101, '2026-03-01'),
(102, '2026-01-01'),
(102, '2026-02-01'),
(103, '2026-02-01'),
(103, '2026-04-01');
```

---

### Day 64 – Human Traffic of Stadium (3+ Consecutive Days with 100+ Visitors)
**Table:** `Stadium`  
**Columns:** `id`, `visit_date`, `people`  

Write a query to display records with three or more rows with consecutive IDs, where the number of people is greater than or equal to 100 for each.

```sql
CREATE TABLE Stadium (
    id INT,
    visit_date DATE,
    people INT
);

INSERT INTO Stadium VALUES
(1, '2026-01-01', 10),
(2, '2026-01-02', 109),
(3, '2026-01-03', 150),
(4, '2026-01-04', 99),
(5, '2026-01-05', 145),
(6, '2026-01-06', 1455),
(7, '2026-01-07', 199),
(8, '2026-01-08', 188);
```

---

### Day 65 – First and Last Touch Attribution
**Table:** `User_Sessions`  
**Columns:** `session_id`, `user_id`, `channel`, `session_time`  

Write a query to find the first marketing channel (`first_touch`) and last marketing channel (`last_touch`) for each user.

```sql
CREATE TABLE User_Sessions (
    session_id INT,
    user_id INT,
    channel VARCHAR(30),
    session_time TIMESTAMP
);

INSERT INTO User_Sessions VALUES
(1, 10, 'Google Ads', '2026-05-01 10:00:00'),
(2, 10, 'Instagram', '2026-05-02 12:30:00'),
(3, 10, 'Direct', '2026-05-05 18:15:00'),
(4, 20, 'Organic', '2026-05-03 09:00:00'),
(5, 20, 'Email', '2026-05-04 14:20:00');
```

---

### Day 66 – Friend Requests: Overall Acceptance Rate
**Table:** `FriendRequest`  
**Columns:** `sender_id`, `send_to_id`, `request_date`  

**Table:** `RequestAccepted`  
**Columns:** `requester_id`, `accepter_id`, `accept_date`  

Write a query to find the overall acceptance rate of requests, which is the number of unique acceptances divided by the number of unique requests (rounded to 2 decimal places).

```sql
CREATE TABLE FriendRequest (
    sender_id INT,
    send_to_id INT,
    request_date DATE
);

INSERT INTO FriendRequest VALUES
(1, 2, '2026-06-01'),
(1, 3, '2026-06-01'),
(1, 4, '2026-06-01'),
(2, 3, '2026-06-02'),
(3, 4, '2026-06-09');

CREATE TABLE RequestAccepted (
    requester_id INT,
    accepter_id INT,
    accept_date DATE
);

INSERT INTO RequestAccepted VALUES
(1, 2, '2026-06-03'),
(1, 3, '2026-06-08'),
(2, 3, '2026-06-08'),
(3, 4, '2026-06-09'),
(3, 4, '2026-06-10');
```

---

### Day 67 – Product Price at a Given Date (Slowly Changing Dimension)
**Table:** `Product_Prices`  
**Columns:** `product_id`, `new_price`, `change_date`  

Write a query to find the prices of all products on `'2026-08-16'`. Assume the price of all products before any change is `10`.

```sql
CREATE TABLE Product_Prices (
    product_id INT,
    new_price INT,
    change_date DATE
);

INSERT INTO Product_Prices VALUES
(1, 20, '2026-08-14'),
(2, 50, '2026-08-14'),
(1, 30, '2026-08-15'),
(1, 35, '2026-08-16'),
(2, 65, '2026-08-17'),
(3, 20, '2026-08-18');
```

---

### Day 68 – Fill Missing Values with Last Non-Null Value (Forward Fill)
**Table:** `Stock_Prices`  
**Columns:** `trade_date`, `close_price`  

Write a query to replace `NULL` values in `close_price` with the most recent previous non-null `close_price`.

```sql
CREATE TABLE Stock_Prices (
    trade_date DATE,
    close_price DECIMAL(10, 2)
);

INSERT INTO Stock_Prices VALUES
('2026-09-01', 150.00),
('2026-09-02', NULL),
('2026-09-03', NULL),
('2026-09-04', 155.50),
('2026-09-05', NULL);
```

---

### Day 69 – Unpivot Columns into Rows
**Table:** `Product_Store_Prices`  
**Columns:** `product_id`, `store1`, `store2`, `store3`  

Write a query to rearrange the `Product_Store_Prices` table so that each row has `(product_id, store, price)`. Exclude rows where the product is not available (`NULL`) in a store.

```sql
CREATE TABLE Product_Store_Prices (
    product_id INT,
    store1 INT,
    store2 INT,
    store3 INT
);

INSERT INTO Product_Store_Prices VALUES
(0, 95, 100, 105),
(1, 70, NULL, 80);
```

---

### Day 70 – Peak Concurrent Sessions (Maximum Simultaneous Users)
**Table:** `Active_Sessions`  
**Columns:** `session_id`, `login_time`, `logout_time`  

Write a query to find the maximum number of users logged in simultaneously at any given moment.

```sql
CREATE TABLE Active_Sessions (
    session_id INT,
    login_time TIMESTAMP,
    logout_time TIMESTAMP
);

INSERT INTO Active_Sessions VALUES
(1, '2026-10-01 09:00:00', '2026-10-01 10:30:00'),
(2, '2026-10-01 09:30:00', '2026-10-01 11:00:00'),
(3, '2026-10-01 10:00:00', '2026-10-01 10:15:00'),
(4, '2026-10-01 10:45:00', '2026-10-01 11:30:00');
```

---

### Day 71 – Clean & Standardize Messy Phone Numbers (Data Cleaning)
**Table:** `Customer_Contacts`  
**Columns:** `customer_id`, `raw_phone`  

Write a query to clean the `raw_phone` column by removing spaces, dashes, and parentheses, and standardize all valid 10-digit numbers into the format `XXX-XXX-XXXX`.

```sql
CREATE TABLE Customer_Contacts (
    customer_id INT,
    raw_phone VARCHAR(30)
);

INSERT INTO Customer_Contacts VALUES
(1, '(987) 654-3210'),
(2, '98765 43211'),
(3, '+91-9876543212'),
(4, '987.654.3213');
```

---

### Day 72 – Business Hours SLA Resolution Time (Date/Time)
**Table:** `Support_Tickets`  
**Columns:** `ticket_id`, `created_at`, `resolved_at`  

Write a query to calculate the total resolution time in hours for each ticket, excluding weekend days (Saturday and Sunday).

```sql
CREATE TABLE Support_Tickets (
    ticket_id INT,
    created_at TIMESTAMP,
    resolved_at TIMESTAMP
);

INSERT INTO Support_Tickets VALUES
(101, '2026-11-06 14:00:00', '2026-11-09 10:00:00'),
(102, '2026-11-04 09:30:00', '2026-11-05 15:30:00'),
(103, '2026-11-07 11:00:00', '2026-11-10 12:00:00');
```

---

### Day 73 – Detect Price Drops Using Window Functions (Window Functions)
**Table:** `Product_History`  
**Columns:** `product_id`, `recorded_date`, `price`  

Write a query to find all dates where a product's price dropped by more than 20% compared to its immediately preceding recorded price.

```sql
CREATE TABLE Product_History (
    product_id INT,
    recorded_date DATE,
    price DECIMAL(10, 2)
);

INSERT INTO Product_History VALUES
(1, '2026-10-01', 100.00),
(1, '2026-10-05', 90.00),
(1, '2026-10-10', 65.00),
(2, '2026-10-01', 200.00),
(2, '2026-10-08', 150.00);
```

---

### Day 74 – Full Outer Join Reconciliation: Bank vs. Ledger (Joins)
**Table:** `Bank_Statements`  
**Columns:** `txn_id`, `amount`  

**Table:** `Internal_Ledger`  
**Columns:** `txn_id`, `amount`  

Write a query to identify all discrepancies between the bank statement and the internal ledger—including transactions missing from either table or transactions where the amounts do not match.

```sql
CREATE TABLE Bank_Statements (
    txn_id INT,
    amount DECIMAL(10, 2)
);

INSERT INTO Bank_Statements VALUES
(1, 500.00),
(2, 1200.00),
(3, 750.00);

CREATE TABLE Internal_Ledger (
    txn_id INT,
    amount DECIMAL(10, 2)
);

INSERT INTO Internal_Ledger VALUES
(1, 500.00),
(2, 1150.00),
(4, 300.00);
```

---

### Day 75 – Split Delimited Tags into Separate Rows (Data Cleaning)
**Table:** `Blog_Posts`  
**Columns:** `post_id`, `tags`  

Write a query to split the comma-separated `tags` string into individual trimmed rows for each `post_id`.

```sql
CREATE TABLE Blog_Posts (
    post_id INT,
    tags VARCHAR(100)
);

INSERT INTO Blog_Posts VALUES
(1, 'sql, data-science, analytics'),
(2, 'python, sql'),
(3, 'etl, data-cleaning, sql');
```

---

### Day 76 – Sessionization: Group Events by 30-Minute Inactivity (Date/Time + Window Functions)
**Table:** `Clickstream`  
**Columns:** `user_id`, `event_time`  

Write a query to assign a `session_id` to each user event, where a new session starts whenever the gap between consecutive events for the same user exceeds 30 minutes.

```sql
CREATE TABLE Clickstream (
    user_id INT,
    event_time TIMESTAMP
);

INSERT INTO Clickstream VALUES
(1, '2026-11-10 08:00:00'),
(1, '2026-11-10 08:15:00'),
(1, '2026-11-10 09:00:00'),
(1, '2026-11-10 09:20:00'),
(2, '2026-11-10 10:00:00'),
(2, '2026-11-10 10:45:00');
```

---

### Day 77 – Find Overlapping Promotions (Self Join)
**Table:** `Promotions`  
**Columns:** `promo_id`, `product_id`, `start_date`, `end_date`  

Write a query to find pairs of promotions for the same product whose active date ranges overlap.

```sql
CREATE TABLE Promotions (
    promo_id INT,
    product_id INT,
    start_date DATE,
    end_date DATE
);

INSERT INTO Promotions VALUES
(1, 10, '2026-07-01', '2026-07-10'),
(2, 10, '2026-07-08', '2026-07-15'),
(3, 10, '2026-07-20', '2026-07-25'),
(4, 20, '2026-07-01', '2026-07-12');
```

---

### Day 78 – Deduplicate Records Keeping Most Complete Row (Data Cleaning)
**Table:** `User_Profiles`  
**Columns:** `user_id`, `email`, `phone`, `city`, `updated_at`  

Write a query to remove duplicate `user_id` entries, keeping the single record per user that has the fewest `NULL` columns (using the latest `updated_at` as a tie-breaker).

```sql
CREATE TABLE User_Profiles (
    user_id INT,
    email VARCHAR(50),
    phone VARCHAR(20),
    city VARCHAR(30),
    updated_at DATE
);

INSERT INTO User_Profiles VALUES
(1, 'a@mail.com', NULL, 'Delhi', '2026-11-01'),
(1, 'a@mail.com', '9999999999', 'Delhi', '2026-10-25'),
(2, NULL, '8888888888', NULL, '2026-11-02'),
(2, 'b@mail.com', '8888888888', NULL, '2026-11-05');
```

---

### Day 79 – Moving Median Over a 3-Day Window (Window Functions)
**Table:** `Daily_Metrics`  
**Columns:** `metric_date`, `value`  

Write a query to compute the 3-day rolling median (current row and 2 preceding rows) for `value` ordered by `metric_date`.

```sql
CREATE TABLE Daily_Metrics (
    metric_date DATE,
    value INT
);

INSERT INTO Daily_Metrics VALUES
('2026-11-01', 10),
('2026-11-02', 40),
('2026-11-03', 20),
('2026-11-04', 50),
('2026-11-05', 30);
```

---

### Day 80 – Anti-Join: Find Orphaned Foreign Keys (Joins + Data Cleaning)
**Table:** `Orders`  
**Columns:** `order_id`, `customer_id`, `order_total`  

**Table:** `Customers`  
**Columns:** `customer_id`, `customer_name`  

Write a query to find all orders whose `customer_id` does not exist in the `Customers` table (including orders where `customer_id` is `NULL`).

```sql
CREATE TABLE Customers (
    customer_id INT,
    customer_name VARCHAR(50)
);

INSERT INTO Customers VALUES
(1, 'Rohan'),
(2, 'Priya');

CREATE TABLE Orders (
    order_id INT,
    customer_id INT,
    order_total DECIMAL(10, 2)
);

INSERT INTO Orders VALUES
(1001, 1, 250.00),
(1002, 99, 400.00),
(1003, NULL, 150.00),
(1004, 2, 600.00);
```

---

### Day 81 – Extract Domain & Standardize Email Casing (Data Cleaning)
**Table:** `User_Signups`  
**Columns:** `user_id`, `raw_email`  

Write a query to trim extra spaces, convert all emails to lowercase, extract the email domain (everything after `@`), and count how many users signed up per domain.

```sql
CREATE TABLE User_Signups (
    user_id INT,
    raw_email VARCHAR(100)
);

INSERT INTO User_Signups VALUES
(1, '  Rahul.Sharma@Gmail.COM '),
(2, 'priya@YAHOO.com'),
(3, 'amit@gmail.com  '),
(4, 'neha@Outlook.com');
```

---

### Day 82 – Generate Missing Calendar Dates (Date/Time + Recursive CTE)
**Table:** `Daily_Sales`  
**Columns:** `sale_date`, `total_amount`  

Write a query to generate a complete date series from `'2026-11-01'` to `'2026-11-07'`, displaying `0` for `total_amount` on dates where no sales occurred.

```sql
CREATE TABLE Daily_Sales (
    sale_date DATE,
    total_amount DECIMAL(10, 2)
);

INSERT INTO Daily_Sales VALUES
('2026-11-01', 500.00),
('2026-11-03', 1200.00),
('2026-11-06', 850.00);
```

---

### Day 83 – Find Employees Who Earned More Than Their Department Average (Window Functions)
**Table:** `Staff_Salaries`  
**Columns:** `emp_id`, `emp_name`, `dept`, `salary`  

Write a query to list all employees whose salary is strictly higher than the average salary of their own department, along with the difference between their salary and the department average.

```sql
CREATE TABLE Staff_Salaries (
    emp_id INT,
    emp_name VARCHAR(50),
    dept VARCHAR(30),
    salary INT
);

INSERT INTO Staff_Salaries VALUES
(1, 'Aarav', 'Engineering', 90000),
(2, 'Diya', 'Engineering', 70000),
(3, 'Kabir', 'Engineering', 80000),
(4, 'Meera', 'HR', 50000),
(5, 'Rohan', 'HR', 60000);
```

---

### Day 84 – Cross Join: Product & Store Availability Matrix (Joins)
**Table:** `Items`  
**Columns:** `item_id`, `item_name`  

**Table:** `Stores`  
**Columns:** `store_id`, `store_city`  

**Table:** `Inventory`  
**Columns:** `store_id`, `item_id`, `stock_qty`  

Write a query to list every possible combination of `store_city` and `item_name`, showing `0` if an item is missing from a store's inventory.

```sql
CREATE TABLE Items (
    item_id INT,
    item_name VARCHAR(50)
);

INSERT INTO Items VALUES (1, 'Mouse'), (2, 'Keyboard');

CREATE TABLE Stores (
    store_id INT,
    store_city VARCHAR(50)
);

INSERT INTO Stores VALUES (10, 'Delhi'), (20, 'Mumbai');

CREATE TABLE Inventory (
    store_id INT,
    item_id INT,
    stock_qty INT
);

INSERT INTO Inventory VALUES
(10, 1, 50),
(20, 2, 30);
```

---

### Day 85 – Convert Mixed Date Formats to Standard ISO Date (Data Cleaning + Date/Time)
**Table:** `Imported_Events`  
**Columns:** `event_id`, `raw_date`  

Write a query to parse the mixed date formats (`YYYY-MM-DD`, `DD/MM/YYYY`, and `Month DD, YYYY`) into a single standardized `DATE` column.

```sql
CREATE TABLE Imported_Events (
    event_id INT,
    raw_date VARCHAR(30)
);

INSERT INTO Imported_Events VALUES
(1, '2026-11-15'),
(2, '18/11/2026'),
(3, 'November 20, 2026');
```

---

### Day 86 – Percentile Rank & Quartile Buckets (Window Functions)
**Table:** `Exam_Scores`  
**Columns:** `student_id`, `student_name`, `score`  

Write a query to assign each student to one of 4 performance quartiles (`1` = Top 25%, `4` = Bottom 25%) and calculate their percentile rank.

```sql
CREATE TABLE Exam_Scores (
    student_id INT,
    student_name VARCHAR(50),
    score INT
);

INSERT INTO Exam_Scores VALUES
(1, 'Ananya', 95),
(2, 'Vikram', 88),
(3, 'Sonia', 76),
(4, 'Karan', 64),
(5, 'Pooja', 91),
(6, 'Dev', 55),
(7, 'Nikhil', 82),
(8, 'Tara', 70);
```

---

### Day 87 – Subscription Active Users on a Specific Date (Date/Time)
**Table:** `Subscriptions`  
**Columns:** `sub_id`, `user_id`, `start_date`, `end_date`  

Write a query to count how many active subscriptions existed on each day between `'2026-11-01'` and `'2026-11-05'`. (An `end_date` of `NULL` means the subscription is still active).

```sql
CREATE TABLE Subscriptions (
    sub_id INT,
    user_id INT,
    start_date DATE,
    end_date DATE
);

INSERT INTO Subscriptions VALUES
(1, 101, '2026-10-25', '2026-11-03'),
(2, 102, '2026-11-02', NULL),
(3, 103, '2026-11-04', '2026-11-05');
```

---

### Day 88 – Conditional Join: Match Orders to Nearest Prior Exchange Rate (Joins + Date/Time)
**Table:** `International_Orders`  
**Columns:** `order_id`, `order_date`, `amount_usd`  

**Table:** `Exchange_Rates`  
**Columns:** `rate_date`, `usd_to_inr`  

Write a query to convert each order's `amount_usd` into INR using the most recent exchange rate available on or before the `order_date`.

```sql
CREATE TABLE International_Orders (
    order_id INT,
    order_date DATE,
    amount_usd DECIMAL(10, 2)
);

INSERT INTO International_Orders VALUES
(1, '2026-11-02', 100.00),
(2, '2026-11-05', 250.00);

CREATE TABLE Exchange_Rates (
    rate_date DATE,
    usd_to_inr DECIMAL(10, 2)
);

INSERT INTO Exchange_Rates VALUES
('2026-11-01', 83.50),
('2026-11-04', 84.00),
('2026-11-06', 84.20);
```

---

### Day 89 – Fuzzy Duplicate Detection: Same Name, Different Spacing/Casing (Data Cleaning)
**Table:** `Company_Directory`  
**Columns:** `company_id`, `company_name`  

Write a query to group and identify duplicate company records that differ only by leading/trailing spaces, multiple internal spaces, or uppercase/lowercase letters.

```sql
CREATE TABLE Company_Directory (
    company_id INT,
    company_name VARCHAR(100)
);

INSERT INTO Company_Directory VALUES
(1, 'Tata Consultancy Services'),
(2, '  tata consultancy   services '),
(3, 'Infosys Limited'),
(4, 'INFOSYS LIMITED');
```

---

### Day 90 – First Value vs. Current Value Growth Comparison (Window Functions)
**Table:** `Portfolio_Value`  
**Columns:** `month_end`, `portfolio_balance`  

Write a query to compare each month's `portfolio_balance` against the very first recorded balance (`2026-01-31`) and calculate the cumulative growth percentage since inception.

```sql
CREATE TABLE Portfolio_Value (
    month_end DATE,
    portfolio_balance DECIMAL(12, 2)
);

INSERT INTO Portfolio_Value VALUES
('2026-01-31', 100000.00),
('2026-02-28', 105000.00),
('2026-03-31', 102000.00),
('2026-04-30', 115000.00);
```

---

### Day 91 – Extract Numbers from Alphanumeric Strings (Data Cleaning)
**Table:** `Product_Descriptions`  
**Columns:** `sku_id`, `description`  

Write a query to extract only the numeric weight value (in grams) from the `description` text and cast it as an integer.

```sql
CREATE TABLE Product_Descriptions (
    sku_id INT,
    description VARCHAR(100)
);

INSERT INTO Product_Descriptions VALUES
(1, 'Organic Almonds Pack - 500g'),
(2, 'Dark Chocolate Bar (150g Net Wt)'),
(3, 'Green Tea Leaves 250g Box');
```

---

### Day 92 – Find Longest Streak of Positive Daily Profit (Window Functions + Date/Time)
**Table:** `Daily_PnL`  
**Columns:** `trade_date`, `net_profit`  

Write a query to find the maximum number of consecutive days where `net_profit` remained strictly positive (`> 0`).

```sql
CREATE TABLE Daily_PnL (
    trade_date DATE,
    net_profit INT
);

INSERT INTO Daily_PnL VALUES
('2026-11-01', 200),
('2026-11-02', 450),
('2026-11-03', -100),
('2026-11-04', 300),
('2026-11-05', 150),
('2026-11-06', 600),
('2026-11-07', -50);
```

---

### Day 93 – Multi-Table Join: Customer Lifetime Value (CLV) Excluding Refunds (Joins)
**Table:** `Customers`  
**Columns:** `cust_id`, `name`  

**Table:** `Orders`  
**Columns:** `order_id`, `cust_id`, `amount`  

**Table:** `Refunds`  
**Columns:** `refund_id`, `order_id`, `refund_amount`  

Write a query to calculate each customer's net lifetime spend (`total_orders - total_refunds`), including customers who have placed zero orders.

```sql
CREATE TABLE Customers (
    cust_id INT,
    name VARCHAR(50)
);

INSERT INTO Customers VALUES (1, 'Arjun'), (2, 'Sneha'), (3, 'Manish');

CREATE TABLE Orders (
    order_id INT,
    cust_id INT,
    amount DECIMAL(10, 2)
);

INSERT INTO Orders VALUES (10, 1, 1000.00), (11, 1, 500.00), (12, 2, 800.00);

CREATE TABLE Refunds (
    refund_id INT,
    order_id INT,
    refund_amount DECIMAL(10, 2)
);

INSERT INTO Refunds VALUES (100, 10, 200.00);
```

---

### Day 94 – Pivot Monthly Revenue by Quarter (Conditional Aggregation)
**Table:** `Monthly_Revenue`  
**Columns:** `rev_date`, `revenue`  

Write a query to aggregate the revenue by year and pivot the quarters into separate columns: `Q1`, `Q2`, `Q3`, and `Q4`.

```sql
CREATE TABLE Monthly_Revenue (
    rev_date DATE,
    revenue INT
);

INSERT INTO Monthly_Revenue VALUES
('2026-01-15', 10000),
('2026-02-20', 12000),
('2026-04-10', 15000),
('2026-07-05', 18000),
('2026-11-12', 22000);
```

---

### Day 95 – Flag Outliers Using Z-Score / Standard Deviation (Window Functions)
**Table:** `Sensor_Readings`  
**Columns:** `reading_id`, `device_id`, `temperature`  

Write a query to flag any reading where the `temperature` is more than 2 standard deviations away from that device's average temperature.

```sql
CREATE TABLE Sensor_Readings (
    reading_id INT,
    device_id INT,
    temperature DECIMAL(5, 2)
);

INSERT INTO Sensor_Readings VALUES
(1, 101, 22.0), (2, 101, 22.5), (3, 101, 21.8),
(4, 101, 22.2), (5, 101, 22.1), (6, 101, 45.0);
```

---

### Day 96 – Merge Overlapping Time Intervals (Date/Time + Window Functions)
**Table:** `Meeting_Rooms`  
**Columns:** `booking_id`, `start_time`, `end_time`  

Write a query to merge overlapping or adjacent meeting bookings into continuous occupied time blocks.

```sql
CREATE TABLE Meeting_Rooms (
    booking_id INT,
    start_time TIMESTAMP,
    end_time TIMESTAMP
);

INSERT INTO Meeting_Rooms VALUES
(1, '2026-11-20 09:00:00', '2026-11-20 10:30:00'),
(2, '2026-11-20 10:00:00', '2026-11-20 11:30:00'),
(3, '2026-11-20 13:00:00', '2026-11-20 14:00:00'),
(4, '2026-11-20 14:00:00', '2026-11-20 15:00:00');
```

---

### Day 97 – Validate & Fix Invalid JSON Strings / Key-Value Parsing (Data Cleaning)
**Table:** `App_Logs`  
**Columns:** `log_id`, `metadata`  

Write a query to parse the `metadata` JSON column and extract `os` and `app_version` into separate columns, replacing missing keys with `'Unknown'`.

```sql
CREATE TABLE App_Logs (
    log_id INT,
    metadata VARCHAR(200)
);

INSERT INTO App_Logs VALUES
(1, '{"os": "Android", "app_version": "2.4.1"}'),
(2, '{"os": "iOS"}'),
(3, '{"app_version": "2.4.0"}');
```

---

### Day 98 – Hierarchies: Find All Subordinates Under a Specific Manager (Recursive Join)
**Table:** `Org_Hierarchy`  
**Columns:** `emp_id`, `emp_name`, `manager_id`  

Write a query to find all direct and indirect subordinates reporting under `'VP Sales'` (`emp_id = 2`).

```sql
CREATE TABLE Org_Hierarchy (
    emp_id INT,
    emp_name VARCHAR(50),
    manager_id INT
);

INSERT INTO Org_Hierarchy VALUES
(1, 'CEO', NULL),
(2, 'VP Sales', 1),
(3, 'VP Tech', 1),
(4, 'Sales Lead', 2),
(5, 'Sales Exec A', 4),
(6, 'Sales Exec B', 4);
```

---

### Day 99 – Cohort Retention Rate Matrix (Date/Time + Window Functions)
**Table:** `User_Activity`  
**Columns:** `user_id`, `activity_date`  

Write a query to group users by their signup month (first `activity_date`) and calculate the percentage of users who returned in Month 1 and Month 2 after signup.

```sql
CREATE TABLE User_Activity (
    user_id INT,
    activity_date DATE
);

INSERT INTO User_Activity VALUES
(1, '2026-01-10'), (1, '2026-02-15'), (1, '2026-03-20'),
(2, '2026-01-12'), (2, '2026-03-05'),
(3, '2026-02-08'), (3, '2026-03-11');
```

---

### Day 100 – End-to-End E-Commerce Funnel & Revenue Attribution (Capstone Challenge)
**Table:** `Events`  
**Columns:** `event_id`, `user_id`, `event_type`, `event_time`  

**Table:** `Purchases`  
**Columns:** `purchase_id`, `user_id`, `revenue`, `purchase_time`  

Write a query to link each purchase to the user's most recent `'ad_click'` event that occurred within 24 hours prior to `purchase_time`, and calculate total attributed revenue vs. unattributed (organic) revenue.

```sql
CREATE TABLE Events (
    event_id INT,
    user_id INT,
    event_type VARCHAR(30),
    event_time TIMESTAMP
);

INSERT INTO Events VALUES
(1, 101, 'ad_click', '2026-11-24 08:00:00'),
(2, 102, 'ad_click', '2026-11-22 09:00:00');

CREATE TABLE Purchases (
    purchase_id INT,
    user_id INT,
    revenue DECIMAL(10, 2),
    purchase_time TIMESTAMP
);

INSERT INTO Purchases VALUES
(501, 101, 1500.00, '2026-11-24 14:00:00'),
(502, 102, 2000.00, '2026-11-24 15:00:00'),
(503, 103, 900.00, '2026-11-24 16:00:00');
```