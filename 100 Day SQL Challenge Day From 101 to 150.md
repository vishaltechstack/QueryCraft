# SQL Practice Problems (Day 101 – Day 150)

A comprehensive collection of 50 intermediate-to-advanced SQL problems covering **Window Functions, Date/Time Manipulation, Complex Joins, and Data Cleaning**.

---

## Day 101 – Running Account Balance & Overdraft Detection (Window Functions)
**Table:** `Bank_Ledger`  
**Columns:** `txn_id`, `account_id`, `txn_time`, `txn_type`, `amount`  

Write a query to calculate the running balance for each `account_id` ordered by `txn_time`, and flag (`'Yes'` / `'No'`) the exact transactions where the balance dropped below `0`.

```sql
CREATE TABLE Bank_Ledger (
    txn_id INT,
    account_id INT,
    txn_time TIMESTAMP,
    txn_type VARCHAR(10),
    amount DECIMAL(10, 2)
);

INSERT INTO Bank_Ledger VALUES
(1, 101, '2026-11-01 09:00:00', 'CREDIT', 1000.00),
(2, 101, '2026-11-02 11:30:00', 'DEBIT', 600.00),
(3, 101, '2026-11-03 14:15:00', 'DEBIT', 550.00),
(4, 101, '2026-11-04 16:00:00', 'CREDIT', 400.00);
```

---

## Day 102 – Identify Undirected Duplicate Pairs (Self Join + Data Cleaning)
**Table:** `Flight_Routes`  
**Columns:** `origin`, `destination`, `distance_km`  

Write a query to deduplicate symmetric flight routes (e.g., `Delhi -> Mumbai` and `Mumbai -> Delhi`) so that only one unique route pair is returned.

```sql
CREATE TABLE Flight_Routes (
    origin VARCHAR(50),
    destination VARCHAR(50),
    distance_km INT
);

INSERT INTO Flight_Routes VALUES
('Delhi', 'Mumbai', 1148),
('Mumbai', 'Delhi', 1148),
('Bengaluru', 'Chennai', 290),
('Chennai', 'Bengaluru', 290),
('Delhi', 'Kolkata', 1305);
```

---

## Day 103 – Detect Data Gaps in Hourly IoT Telemetry (Date/Time + Window Functions)
**Table:** `IoT_Heartbeats`  
**Columns:** `device_id`, `ping_time`  

Write a query to detect missing hourly heartbeats for each device by returning the `device_id`, `missing_start_time`, and `missing_end_time` whenever the gap between consecutive pings is greater than 1 hour.

```sql
CREATE TABLE IoT_Heartbeats (
    device_id INT,
    ping_time TIMESTAMP
);

INSERT INTO IoT_Heartbeats VALUES
(1, '2026-11-20 08:00:00'),
(1, '2026-11-20 09:00:00'),
(1, '2026-11-20 12:00:00'),
(1, '2026-11-20 13:00:00'),
(2, '2026-11-20 10:00:00'),
(2, '2026-11-20 14:00:00');
```

---

## Day 104 – FIFO Inventory Valuation (Window Functions + Joins)
**Table:** `Stock_Purchases`  
**Columns:** `batch_id`, `purchase_date`, `qty`, `unit_cost`  

**Table:** `Stock_Sales`  
**Columns:** `sale_id`, `sale_date`, `qty_sold`  

Write a query using First-In, First-Out (FIFO) logic to calculate the Cost of Goods Sold (COGS) and remaining inventory value after all sales.

```sql
CREATE TABLE Stock_Purchases (
    batch_id INT,
    purchase_date DATE,
    qty INT,
    unit_cost DECIMAL(10, 2)
);

INSERT INTO Stock_Purchases VALUES
(1, '2026-10-01', 100, 10.00),
(2, '2026-10-10', 100, 12.00),
(3, '2026-10-20', 100, 15.00);

CREATE TABLE Stock_Sales (
    sale_id INT,
    sale_date DATE,
    qty_sold INT
);

INSERT INTO Stock_Sales VALUES
(101, '2026-10-25', 150);
```

---

## Day 105 – Normalize Split Name Columns & Handle Middle Names (Data Cleaning)
**Table:** `Raw_Customers`  
**Columns:** `id`, `full_name`  

Write a query to split `full_name` into `first_name`, `middle_name` (set to `NULL` if none exists), and `last_name` after removing extra whitespace.

```sql
CREATE TABLE Raw_Customers (
    id INT,
    full_name VARCHAR(100)
);

INSERT INTO Raw_Customers VALUES
(1, 'Amit Kumar Sharma'),
(2, '  Priya Verma '),
(3, 'Rohan Singhania'),
(4, 'Sonia Devi Gupta');
```

---

## Day 106 – Time-Weighted Average Price (TWAP) (Date/Time + Window Functions)
**Table:** `Crypto_Ticks`  
**Columns:** `tick_time`, `price`  

Write a query to calculate the Time-Weighted Average Price (TWAP) between `'2026-11-24 10:00:00'` and `'2026-11-24 11:00:00'`, weighting each price by the number of minutes it remained active.

```sql
CREATE TABLE Crypto_Ticks (
    tick_time TIMESTAMP,
    price DECIMAL(10, 2)
);

INSERT INTO Crypto_Ticks VALUES
('2026-11-24 10:00:00', 50000.00),
('2026-11-24 10:15:00', 52000.00),
('2026-11-24 10:45:00', 51000.00),
('2026-11-24 11:00:00', 53000.00);
```

---

## Day 107 – Find Most Common Co-Occurring Tag Pair (Self Join)
**Table:** `Article_Tags`  
**Columns:** `article_id`, `tag`  

Write a query to find the pair of tags that appear together on the highest number of articles, ordered alphabetically within each pair `(tag1 < tag2)`.

```sql
CREATE TABLE Article_Tags (
    article_id INT,
    tag VARCHAR(30)
);

INSERT INTO Article_Tags VALUES
(1, 'SQL'), (1, 'Python'), (1, 'ETL'),
(2, 'SQL'), (2, 'Python'),
(3, 'SQL'), (3, 'ETL'),
(4, 'Python'), (4, 'ML');
```

---

## Day 108 – Identify Sudden Spikes Compared to Previous 7-Day Average (Window Functions)
**Table:** `Server_Requests`  
**Columns:** `req_date`, `request_count`  

Write a query to find dates where `request_count` was at least 3 times higher than the rolling average of the preceding 7 days (excluding the current day).

```sql
CREATE TABLE Server_Requests (
    req_date DATE,
    request_count INT
);

INSERT INTO Server_Requests VALUES
('2026-11-01', 100), ('2026-11-02', 110), ('2026-11-03', 95),
('2026-11-04', 105), ('2026-11-05', 100), ('2026-11-06', 115),
('2026-11-07', 90),  ('2026-11-08', 450);
```

---

## Day 109 – Coalesce & Merge Incremental Data Updates (Joins + Data Cleaning)
**Table:** `Master_Users`  
**Columns:** `user_id`, `email`, `city`, `tier`  

**Table:** `Daily_Delta`  
**Columns:** `user_id`, `email`, `city`, `tier`  

Write a query to produce the updated master user list by merging `Daily_Delta` into `Master_Users`—updating existing users only for non-null columns in `Daily_Delta`, and inserting brand-new users.

```sql
CREATE TABLE Master_Users (
    user_id INT,
    email VARCHAR(50),
    city VARCHAR(30),
    tier VARCHAR(20)
);

INSERT INTO Master_Users VALUES
(1, 'rahul@mail.com', 'Delhi', 'Free'),
(2, 'neha@mail.com', 'Pune', 'Pro');

CREATE TABLE Daily_Delta (
    user_id INT,
    email VARCHAR(50),
    city VARCHAR(30),
    tier VARCHAR(20)
);

INSERT INTO Daily_Delta VALUES
(1, NULL, 'Bengaluru', 'Pro'),
(3, 'kiran@mail.com', 'Hyderabad', 'Free');
```

---

## Day 110 – Find Second Most Recent Activity Per User (Fallback to First if Only One Exists)
**Table:** `User_Logs`  
**Columns:** `user_id`, `activity`, `activity_date`  

Write a query to return each user's second most recent activity. If a user has only one recorded activity, return that single activity instead.

```sql
CREATE TABLE User_Logs (
    user_id INT,
    activity VARCHAR(50),
    activity_date DATE
);

INSERT INTO User_Logs VALUES
(1, 'Login', '2026-11-01'),
(1, 'Search', '2026-11-02'),
(1, 'Checkout', '2026-11-03'),
(2, 'Login', '2026-11-05');
```

---

## Day 111 – Parse & Flatten URL Query Parameters (Data Cleaning)
**Table:** `Web_Traffic`  
**Columns:** `hit_id`, `full_url`  

Write a query to extract the `utm_source` and `utm_campaign` values from the query string of `full_url` (returning `NULL` if a parameter is missing).

```sql
CREATE TABLE Web_Traffic (
    hit_id INT,
    full_url VARCHAR(255)
);

INSERT INTO Web_Traffic VALUES
(1, 'https://example.com/shop?utm_source=google&utm_campaign=diwali_sale&ref=123'),
(2, 'https://example.com/blog?utm_source=linkedin'),
(3, 'https://example.com/home');
```

---

## Day 112 – Calculate Age in Exact Years, Months, and Days (Date/Time)
**Table:** `Employees_DOB`  
**Columns:** `emp_id`, `emp_name`, `birth_date`  

Write a query to calculate each employee's exact age in years, months, and days as of `'2026-11-24'`.

```sql
CREATE TABLE Employees_DOB (
    emp_id INT,
    emp_name VARCHAR(50),
    birth_date DATE
);

INSERT INTO Employees_DOB VALUES
(1, 'Aarav', '1995-05-15'),
(2, 'Kavya', '1998-12-10'),
(3, 'Rohan', '2000-11-24');
```

---

## Day 113 – Exponential Moving Average (EMA) Calculation (Window Functions + Recursive CTE)
**Table:** `Stock_Close`  
**Columns:** `day_num`, `trade_date`, `close_price`  

Write a query to compute the 3-day Exponential Moving Average (EMA) where $\alpha = \frac{2}{3 + 1} = 0.5$, starting with Day 1's `close_price` as the initial EMA.

```sql
CREATE TABLE Stock_Close (
    day_num INT,
    trade_date DATE,
    close_price DECIMAL(10, 2)
);

INSERT INTO Stock_Close VALUES
(1, '2026-11-18', 100.00),
(2, '2026-11-19', 110.00),
(3, '2026-11-20', 105.00),
(4, '2026-11-23', 120.00);
```

---

## Day 114 – Range Join: Assign Pricing Tier Based on Order Volume (Joins)
**Table:** `Bulk_Orders`  
**Columns:** `order_id`, `quantity`  

**Table:** `Discount_Tiers`  
**Columns:** `tier_name`, `min_qty`, `max_qty`, `discount_pct`  

Write a query to match each order to its corresponding discount tier based on `quantity` and compute the final `discount_pct` (`max_qty` is `NULL` for the highest unlimited tier).

```sql
CREATE TABLE Bulk_Orders (
    order_id INT,
    quantity INT
);

INSERT INTO Bulk_Orders VALUES
(1, 5),
(2, 25),
(3, 120);

CREATE TABLE Discount_Tiers (
    tier_name VARCHAR(20),
    min_qty INT,
    max_qty INT,
    discount_pct INT
);

INSERT INTO Discount_Tiers VALUES
('Standard', 1, 10, 0),
('Silver', 11, 50, 10),
('Gold', 51, NULL, 20);
```

---

## Day 115 – Strip Non-Numeric Characters & Standardize Currency Values (Data Cleaning)
**Table:** `Raw_Invoices`  
**Columns:** `invoice_id`, `raw_amount`  

Write a query to remove currency symbols (`₹`, `$`), commas, and whitespace from `raw_amount`, and cast the cleaned values into a `DECIMAL(10, 2)` column.

```sql
CREATE TABLE Raw_Invoices (
    invoice_id INT,
    raw_amount VARCHAR(30)
);

INSERT INTO Raw_Invoices VALUES
(1, '₹ 1,25,000.50'),
(2, '$4,500.00 '),
(3, '  890.75 INR');
```

---

## Day 116 – Identify Weekend vs. Weekday Conversion Lift (Date/Time)
**Table:** `Checkout_Attempts`  
**Columns:** `attempt_id`, `attempt_time`, `is_completed`  

Write a query to compare the conversion rate (`SUM(is_completed) / COUNT(*)`) between Weekdays (Monday–Friday) and Weekends (Saturday–Sunday).

```sql
CREATE TABLE Checkout_Attempts (
    attempt_id INT,
    attempt_time TIMESTAMP,
    is_completed INT
);

INSERT INTO Checkout_Attempts VALUES
(1, '2026-11-20 11:00:00', 1),
(2, '2026-11-20 15:00:00', 0),
(3, '2026-11-21 10:30:00', 1),
(4, '2026-11-22 18:45:00', 1),
(5, '2026-11-23 09:15:00', 0);
```

---

## Day 117 – Find Top Performer per Group Excluding Ties (Window Functions)
**Table:** `Sales_Leaderboard`  
**Columns:** `region`, `rep_name`, `deals_closed`  

Write a query to find the sole top-performing sales rep in each region. If two or more reps tie for the highest `deals_closed` in a region, exclude that region from the output.

```sql
CREATE TABLE Sales_Leaderboard (
    region VARCHAR(30),
    rep_name VARCHAR(50),
    deals_closed INT
);

INSERT INTO Sales_Leaderboard VALUES
('North', 'Anil', 15),
('North', 'Sunita', 12),
('South', 'Karthik', 20),
('South', 'Meena', 20),
('West', 'Pooja', 18);
```

---

## Day 118 – Self Join: Detect Circular Manager Loops in Hierarchy (Joins + Data Cleaning)
**Table:** `Bad_Hierarchy`  
**Columns:** `emp_id`, `manager_id`  

Write a query to identify broken/circular reporting loops where two employees are listed as each other's direct manager (`A -> B` and `B -> A`).

```sql
CREATE TABLE Bad_Hierarchy (
    emp_id INT,
    manager_id INT
);

INSERT INTO Bad_Hierarchy VALUES
(1, NULL),
(2, 1),
(3, 4),
(4, 3),
(5, 2);
```

---

## Day 119 – Normalize Multi-Value Delimited Pairs into Key-Value Table (Data Cleaning)
**Table:** `Product_Specs`  
**Columns:** `product_id`, `specs_string`  

Write a query to parse the semicolon-separated `key:value` pairs in `specs_string` into individual rows with columns `(product_id, spec_key, spec_value)`.

```sql
CREATE TABLE Product_Specs (
    product_id INT,
    specs_string VARCHAR(150)
);

INSERT INTO Product_Specs VALUES
(101, 'Color:Black;RAM:16GB;Storage:512GB'),
(102, 'Color:Silver;RAM:8GB');
```

---

## Day 120 – Identify First Purchase That Crossed ₹10,000 Cumulative Spend (Window Functions)
**Table:** `Customer_Spend`  
**Columns:** `txn_id`, `customer_id`, `txn_date`, `amount`  

Write a query to find the exact `txn_id` and `txn_date` on which each customer's cumulative spend first reached or exceeded `10000`.

```sql
CREATE TABLE Customer_Spend (
    txn_id INT,
    customer_id INT,
    txn_date DATE,
    amount INT
);

INSERT INTO Customer_Spend VALUES
(1, 10, '2026-10-01', 4000),
(2, 10, '2026-10-05', 3500),
(3, 10, '2026-10-12', 3000),
(4, 10, '2026-10-20', 5000),
(5, 20, '2026-10-02', 6000),
(6, 20, '2026-10-10', 2000);
```

---

## Day 121 – Detect & Remove Duplicate Adjacent Events (Window Functions + Data Cleaning)
**Table:** `Button_Clicks`  
**Columns:** `click_id`, `user_id`, `page_name`, `click_time`  

Write a query to compress consecutive duplicate page visits for the same user (e.g., `Home -> Home -> Cart -> Home` becomes `Home -> Cart -> Home`), keeping only the first timestamp of each consecutive streak.

```sql
CREATE TABLE Button_Clicks (
    click_id INT,
    user_id INT,
    page_name VARCHAR(30),
    click_time TIMESTAMP
);

INSERT INTO Button_Clicks VALUES
(1, 10, 'Home', '2026-11-24 10:00:00'),
(2, 10, 'Home', '2026-11-24 10:00:05'),
(3, 10, 'Cart', '2026-11-24 10:01:00'),
(4, 10, 'Home', '2026-11-24 10:02:00');
```

---

## Day 122 – Calculate Fiscal Year & Fiscal Quarter (Date/Time)
**Table:** `Corporate_Sales`  
**Columns:** `sale_id`, `sale_date`, `amount`  

Write a query to map each `sale_date` to the Indian Fiscal Year (April 1 to March 31, e.g., `'2026-05-10'` belongs to `'FY2026-27'`) and Fiscal Quarter (`Q1` = Apr–Jun, `Q2` = Jul–Sep, `Q3` = Oct–Dec, `Q4` = Jan–Mar), then sum the total sales per Fiscal Year and Quarter.

```sql
CREATE TABLE Corporate_Sales (
    sale_id INT,
    sale_date DATE,
    amount INT
);

INSERT INTO Corporate_Sales VALUES
(1, '2026-02-15', 50000),
(2, '2026-04-10', 70000),
(3, '2026-08-20', 60000),
(4, '2026-11-24', 90000);
```

---

## Day 123 – Semi-Join: Customers Who Ordered Electronics But Never Accessories (Joins)
**Table:** `Customer_Orders`  
**Columns:** `order_id`, `customer_id`, `category`  

Write a query to find all `customer_id` values that have purchased at least one item from `'Electronics'` and have **never** purchased anything from `'Accessories'`.

```sql
CREATE TABLE Customer_Orders (
    order_id INT,
    customer_id INT,
    category VARCHAR(30)
);

INSERT INTO Customer_Orders VALUES
(1, 101, 'Electronics'),
(2, 101, 'Books'),
(3, 102, 'Electronics'),
(4, 102, 'Accessories'),
(5, 103, 'Accessories');
```

---

## Day 124 – Calculate Weighted Moving Average (Window Functions)
**Table:** `Demand_Forecast`  
**Columns:** `week_num`, `units_sold`  

Write a query to compute the 3-week Weighted Moving Average (WMA) for `units_sold` starting from Week 3, assigning weights of `0.5` to the current week, `0.3` to 1 week prior, and `0.2` to 2 weeks prior.

```sql
CREATE TABLE Demand_Forecast (
    week_num INT,
    units_sold INT
);

INSERT INTO Demand_Forecast VALUES
(1, 100),
(2, 120),
(3, 150),
(4, 140),
(5, 180);
```

---

## Day 125 – Mask Sensitive PII Data (Email & Phone) (Data Cleaning)
**Table:** `Customer_PII`  
**Columns:** `cust_id`, `email`, `phone`  

Write a query to mask `email` by showing only the first 2 characters followed by `***` before the `@` domain (e.g., `ra***@gmail.com`), and mask `phone` to show only the last 4 digits (`******3210`).

```sql
CREATE TABLE Customer_PII (
    cust_id INT,
    email VARCHAR(60),
    phone VARCHAR(15)
);

INSERT INTO Customer_PII VALUES
(1, 'rahul.verma@gmail.com', '9876543210'),
(2, 'ananya@outlook.com', '9123456789');
```

---

## Day 126 – Find Peak Concurrent Delivery Drivers Per Hour (Date/Time + Window Functions)
**Table:** `Delivery_Shifts`  
**Columns:** `driver_id`, `shift_start`, `shift_end`  

Write a query to find how many drivers were actively on shift during each hour of `'2026-11-24'` (from `08:00` to `13:00`).

```sql
CREATE TABLE Delivery_Shifts (
    driver_id INT,
    shift_start TIMESTAMP,
    shift_end TIMESTAMP
);

INSERT INTO Delivery_Shifts VALUES
(1, '2026-11-24 08:00:00', '2026-11-24 12:00:00'),
(2, '2026-11-24 09:30:00', '2026-11-24 13:00:00'),
(3, '2026-11-24 10:00:00', '2026-11-24 11:30:00');
```

---

## Day 127 – Lateral Join / Top-N Per Group Without Window Functions (Joins)
**Table:** `Categories`  
**Columns:** `cat_id`, `cat_name`  

**Table:** `Products`  
**Columns:** `prod_id`, `cat_id`, `prod_name`, `rating`  

Write a query using a `LATERAL` join (or correlated subquery) to retrieve the top 2 highest-rated products for each category, including categories with fewer than 2 products.

```sql
CREATE TABLE Categories (
    cat_id INT,
    cat_name VARCHAR(30)
);

INSERT INTO Categories VALUES (1, 'Mobiles'), (2, 'Laptops');

CREATE TABLE Products (
    prod_id INT,
    cat_id INT,
    prod_name VARCHAR(50),
    rating DECIMAL(3, 2)
);

INSERT INTO Products VALUES
(10, 1, 'Phone A', 4.80),
(11, 1, 'Phone B', 4.50),
(12, 1, 'Phone C', 4.90),
(13, 2, 'Laptop X', 4.70);
```

---

## Day 128 – Standardize Boolean & Status Flags Across Legacy Systems (Data Cleaning)
**Table:** `Legacy_Accounts`  
**Columns:** `acc_id`, `is_active_raw`  

Write a query to normalize the messy `is_active_raw` values (`'Y'`, `'yes'`, `'1'`, `'True'`, `'N'`, `'0'`, `'false'`, `NULL`) into a clean boolean/integer flag (`1` for active, `0` for inactive/unknown).

```sql
CREATE TABLE Legacy_Accounts (
    acc_id INT,
    is_active_raw VARCHAR(20)
);

INSERT INTO Legacy_Accounts VALUES
(1, 'Y'),
(2, '  true '),
(3, '1'),
(4, 'No'),
(5, '0'),
(6, NULL);
```

---

## Day 129 – Detect Streaks of Missed Targets (Gaps & Islands with Window Functions)
**Table:** `Monthly_KPIs`  
**Columns:** `rep_id`, `kpi_month`, `target_met`  

Write a query to find reps who failed to meet their target (`target_met = 0`) for 3 or more consecutive months, along with the start and end month of each missed streak.

```sql
CREATE TABLE Monthly_KPIs (
    rep_id INT,
    kpi_month DATE,
    target_met INT
);

INSERT INTO Monthly_KPIs VALUES
(1, '2026-06-01', 0),
(1, '2026-07-01', 0),
(1, '2026-08-01', 0),
(1, '2026-09-01', 1),
(2, '2026-06-01', 0),
(2, '2026-07-01', 1),
(2, '2026-08-01', 0);
```

---

## Day 130 – Reconcile Multi-Currency Daily Revenue to Base Currency (Joins + Date/Time)
**Table:** `Global_Sales`  
**Columns:** `sale_id`, `sale_date`, `currency`, `amount`  

**Table:** `FX_Rates`  
**Columns:** `fx_date`, `currency`, `rate_to_inr`  

Write a query to compute the total daily revenue in INR across all currencies, assuming INR transactions have a `1.0` rate and missing weekend FX rates carry forward from Friday's rate.

```sql
CREATE TABLE Global_Sales (
    sale_id INT,
    sale_date DATE,
    currency VARCHAR(5),
    amount DECIMAL(10, 2)
);

INSERT INTO Global_Sales VALUES
(1, '2026-11-20', 'USD', 100.00),
(2, '2026-11-21', 'USD', 200.00),
(3, '2026-11-21', 'EUR', 150.00),
(4, '2026-11-21', 'INR', 5000.00);

CREATE TABLE FX_Rates (
    fx_date DATE,
    currency VARCHAR(5),
    rate_to_inr DECIMAL(10, 2)
);

INSERT INTO FX_Rates VALUES
('2026-11-20', 'USD', 84.00),
('2026-11-20', 'EUR', 90.00);
```

---

## Day 131 – Extract & Normalize Valid Indian PIN Codes (Data Cleaning)
**Table:** `Shipping_Addresses`  
**Columns:** `address_id`, `raw_address`  

Write a query to extract the 6-digit Indian PIN code from `raw_address` (ignoring spaces inside the digits like `110 001` and returning `NULL` if no valid 6-digit PIN code exists).

```sql
CREATE TABLE Shipping_Addresses (
    address_id INT,
    raw_address VARCHAR(150)
);

INSERT INTO Shipping_Addresses VALUES
(1, 'Connaught Place, New Delhi - 110001'),
(2, 'Andheri West, Mumbai 400 058, India'),
(3, 'MG Road, Bengaluru (No PIN)'),
(4, 'Sector 18, Noida, UP-201301');
```

---

## Day 132 – Calculate Active Working Minutes Between Two Timestamps (Date/Time)
**Table:** `Agent_Tickets`  
**Columns:** `ticket_id`, `opened_at`, `closed_at`  

Write a query to calculate the exact number of working minutes between `opened_at` and `closed_at`, counting only business hours (`09:00` to `18:00`) on Monday through Friday.

```sql
CREATE TABLE Agent_Tickets (
    ticket_id INT,
    opened_at TIMESTAMP,
    closed_at TIMESTAMP
);

INSERT INTO Agent_Tickets VALUES
(1, '2026-11-20 16:30:00', '2026-11-23 10:30:00'),
(2, '2026-11-24 11:00:00', '2026-11-24 14:15:00');
```

---

## Day 133 – Calculate Rolling 3-Order Average Excluding Current Order (Window Functions)
**Table:** `Customer_Purchases`  
**Columns:** `order_id`, `customer_id`, `order_date`, `order_amount`  

Write a query to compute each customer's average spend across their **preceding 3 orders** (strictly excluding the current order), showing `NULL` for their very first order.

```sql
CREATE TABLE Customer_Purchases (
    order_id INT,
    customer_id INT,
    order_date DATE,
    order_amount DECIMAL(10, 2)
);

INSERT INTO Customer_Purchases VALUES
(1, 10, '2026-10-01', 200.00),
(2, 10, '2026-10-05', 400.00),
(3, 10, '2026-10-10', 600.00),
(4, 10, '2026-10-15', 800.00),
(5, 10, '2026-10-20', 1000.00);
```

---

## Day 134 – Asymmetric Join: Match Call Logs to Nearest Support Agent Shift (Joins + Date/Time)
**Table:** `Support_Calls`  
**Columns:** `call_id`, `agent_id`, `call_time`  

**Table:** `Shift_Roster`  
**Columns:** `shift_id`, `agent_id`, `shift_start`, `shift_end`  

Write a query to join each call with the corresponding shift record where `call_time` falls between `shift_start` and `shift_end`, and flag calls that occurred outside any scheduled shift as `'Unscheduled'`.

```sql
CREATE TABLE Support_Calls (
    call_id INT,
    agent_id INT,
    call_time TIMESTAMP
);

INSERT INTO Support_Calls VALUES
(101, 1, '2026-11-24 10:15:00'),
(102, 1, '2026-11-24 19:30:00'),
(103, 2, '2026-11-24 14:00:00');

CREATE TABLE Shift_Roster (
    shift_id INT,
    agent_id INT,
    shift_start TIMESTAMP,
    shift_end TIMESTAMP
);

INSERT INTO Shift_Roster VALUES
(1, 1, '2026-11-24 09:00:00', '2026-11-24 17:00:00'),
(2, 2, '2026-11-24 12:00:00', '2026-11-24 20:00:00');
```

---

## Day 135 – Resolve Conflicting Master Records by Source Priority (Data Cleaning + Window Functions)
**Table:** `CRM_Contacts`  
**Columns:** `contact_id`, `email`, `source_system`, `phone`, `updated_at`  

Write a query to deduplicate contacts by `email`, prioritizing records based on source reliability (`'ERP'` > `'Salesforce'` > `'WebForm'`), and using `updated_at DESC` as a tie-breaker.

```sql
CREATE TABLE CRM_Contacts (
    contact_id INT,
    email VARCHAR(60),
    source_system VARCHAR(20),
    phone VARCHAR(15),
    updated_at DATE
);

INSERT INTO CRM_Contacts VALUES
(1, 'vikas@company.com', 'WebForm', '9000011111', '2026-11-24'),
(2, 'vikas@company.com', 'ERP', '9000022222', '2026-11-20'),
(3, 'meera@company.com', 'Salesforce', '9000033333', '2026-11-22'),
(4, 'meera@company.com', 'WebForm', '9000044444', '2026-11-23');
```

---

## Day 136 – Calculate Month-to-Date (MTD) vs. Prior Month-to-Date (PMTD) Sales (Date/Time + Window Functions)
**Table:** `Daily_Revenue`  
**Columns:** `rev_date`, `revenue`  

Write a query to compare the cumulative Month-to-Date (MTD) revenue up to `'2026-11-15'` against the exact same period in the prior month (`'2026-10-01'` to `'2026-10-15'`).

```sql
CREATE TABLE Daily_Revenue (
    rev_date DATE,
    revenue INT
);

INSERT INTO Daily_Revenue VALUES
('2026-10-05', 10000),
('2026-10-15', 15000),
('2026-10-25', 20000),
('2026-11-04', 12000),
('2026-11-15', 18000);
```

---

## Day 137 – Full Outer Join with Coalesced Keys: Monthly Budget vs. Actuals (Joins)
**Table:** `Department_Budget`  
**Columns:** `dept`, `month_num`, `budget_amount`  

**Table:** `Department_Actuals`  
**Columns:** `dept`, `month_num`, `actual_amount`  

Write a query to produce a complete variance report (`actual_amount - budget_amount`) across all departments and months, handling cases where a department had a budget with zero actual spend or actual spend with zero budget.

```sql
CREATE TABLE Department_Budget (
    dept VARCHAR(30),
    month_num INT,
    budget_amount INT
);

INSERT INTO Department_Budget VALUES
('Marketing', 11, 50000),
('R&D', 11, 80000);

CREATE TABLE Department_Actuals (
    dept VARCHAR(30),
    month_num INT,
    actual_amount INT
);

INSERT INTO Department_Actuals VALUES
('Marketing', 11, 55000),
('Operations', 11, 30000);
```

---

## Day 138 – Detect Sequential Gaps & Reset Group Counters (Window Functions)
**Table:** `Machine_Events`  
**Columns:** `event_id`, `machine_id`, `status`, `event_time`  

Write a query to count how many consecutive `'OK'` events occurred before each `'ERROR'` event per machine (resetting the counter to `0` after every `'ERROR'`).

```sql
CREATE TABLE Machine_Events (
    event_id INT,
    machine_id INT,
    status VARCHAR(10),
    event_time TIMESTAMP
);

INSERT INTO Machine_Events VALUES
(1, 101, 'OK', '2026-11-24 08:00:00'),
(2, 101, 'OK', '2026-11-24 08:05:00'),
(3, 101, 'ERROR', '2026-11-24 08:10:00'),
(4, 101, 'OK', '2026-11-24 08:15:00'),
(5, 101, 'ERROR', '2026-11-24 08:20:00');
```

---

## Day 139 – Clean HTML Tags & Decode Special Characters from Text (Data Cleaning)
**Table:** `Product_Reviews`  
**Columns:** `review_id`, `raw_comment`  

Write a query to strip all HTML tags (e.g., `<p>`, `<br>`, `<b>`) and replace `&amp;` with `&` in `raw_comment`, trimming extra whitespace.

```sql
CREATE TABLE Product_Reviews (
    review_id INT,
    raw_comment VARCHAR(200)
);

INSERT INTO Product_Reviews VALUES
(1, '<p>Great product &amp; <b>fast</b> delivery!</p>'),
(2, '  Good quality<br>Worth the price.  ');
```

---

## Day 140 – Anti-Join & Self-Comparison: Products Never Sold Together (Joins)
**Table:** `Menu_Items`  
**Columns:** `item_name`  

**Table:** `Order_Details`  
**Columns:** `order_id`, `item_name`  

Write a query to find all unique pairs of menu items `(item1 < item2)` that have **never** appeared together in the same order.

```sql
CREATE TABLE Menu_Items (
    item_name VARCHAR(30)
);

INSERT INTO Menu_Items VALUES ('Burger'), ('Fries'), ('Salad');

CREATE TABLE Order_Details (
    order_id INT,
    item_name VARCHAR(30)
);

INSERT INTO Order_Details VALUES
(1, 'Burger'), (1, 'Fries'),
(2, 'Fries'), (2, 'Salad');
```

---

## Day 141 – Normalize JSON Array Elements into Individual Rows (Data Cleaning)
**Table:** `Order_Events`  
**Columns:** `order_id`, `applied_coupons`  

Write a query to unpack the JSON array in `applied_coupons` so that each coupon code appears on a separate row alongside its `order_id` (excluding orders with empty arrays `[]`).

```sql
CREATE TABLE Order_Events (
    order_id INT,
    applied_coupons VARCHAR(150)
);

INSERT INTO Order_Events VALUES
(101, '["WELCOME10", "FREESHIP"]'),
(102, '["FESTIVE20"]'),
(103, '[]');
```

---

## Day 142 – Calculate Rolling 30-Day Active Users (DAU/MAU Stickiness Ratio) (Date/Time + Window Functions)
**Table:** `User_Logins`  
**Columns:** `user_id`, `login_date`  

Write a query to calculate the Daily Active Users (DAU) for each date, the rolling 30-day unique active users (MAU), and the stickiness ratio (`DAU / MAU`).

```sql
CREATE TABLE User_Logins (
    user_id INT,
    login_date DATE
);

INSERT INTO User_Logins VALUES
(1, '2026-11-01'), (2, '2026-11-01'),
(1, '2026-11-15'), (3, '2026-11-15'),
(1, '2026-11-24'), (2, '2026-11-24'), (4, '2026-11-24');
```

---

## Day 143 – Detect Out-of-Sequence Events Using Window Functions (Window Functions + Date/Time)
**Table:** `Shipment_Tracking`  
**Columns:** `tracking_id`, `parcel_id`, `status`, `status_time`  

Write a query to identify parcels where the `'Delivered'` status timestamp is recorded earlier than the `'Dispatched'` status timestamp due to system clock sync errors.

```sql
CREATE TABLE Shipment_Tracking (
    tracking_id INT,
    parcel_id INT,
    status VARCHAR(20),
    status_time TIMESTAMP
);

INSERT INTO Shipment_Tracking VALUES
(1, 501, 'Dispatched', '2026-11-20 10:00:00'),
(2, 501, 'Delivered', '2026-11-21 14:00:00'),
(3, 502, 'Dispatched', '2026-11-22 15:00:00'),
(4, 502, 'Delivered', '2026-11-22 12:30:00');
```

---

## Day 144 – Left Join with Pre-Aggregated Subquery to Avoid Fan-Out (Joins)
**Table:** `Campaigns`  
**Columns:** `campaign_id`, `campaign_name`, `budget`  

**Table:** `Ad_Clicks`  
**Columns:** `click_id`, `campaign_id`  

**Table:** `Ad_Conversions`  
**Columns:** `conv_id`, `campaign_id`, `revenue`  

Write a query to report each campaign's `budget`, total `clicks`, and total `revenue` without duplicating rows (fan-out) when joining two 1-to-many child tables.

```sql
CREATE TABLE Campaigns (
    campaign_id INT,
    campaign_name VARCHAR(50),
    budget INT
);

INSERT INTO Campaigns VALUES (1, 'Diwali Search', 10000), (2, 'Winter Display', 5000);

CREATE TABLE Ad_Clicks (
    click_id INT,
    campaign_id INT
);

INSERT INTO Ad_Clicks VALUES (1, 1), (2, 1), (3, 1), (4, 2);

CREATE TABLE Ad_Conversions (
    conv_id INT,
    campaign_id INT,
    revenue INT
);

INSERT INTO Ad_Conversions VALUES (10, 1, 4000), (11, 1, 6000);
```

---

## Day 145 – Standardize State Names & Abbreviations (Data Cleaning)
**Table:** `Customer_Locations`  
**Columns:** `cust_id`, `raw_state`  

Write a query to clean and standardize `raw_state` values (`'DL'`, `'New Delhi'`, `'delhi'` -> `'Delhi'`; `'MH'`, `'maharashtra'` -> `'Maharashtra'`; `'KA'`, `'Karnataka'` -> `'Karnataka'`), grouping all unknown entries as `'Other'`.

```sql
CREATE TABLE Customer_Locations (
    cust_id INT,
    raw_state VARCHAR(30)
);

INSERT INTO Customer_Locations VALUES
(1, 'DL'),
(2, '  New Delhi '),
(3, 'mh'),
(4, 'Karnataka'),
(5, 'Goa');
```

---

## Day 146 – Find Next Business Day After a Holiday/Weekend (Date/Time)
**Table:** `Invoices`  
**Columns:** `invoice_id`, `due_date`  

**Table:** `Public_Holidays`  
**Columns:** `holiday_date`  

Write a query to adjust each `due_date`: if a `due_date` falls on a Saturday, Sunday, or a date listed in `Public_Holidays`, shift it forward to the next valid working day.

```sql
CREATE TABLE Invoices (
    invoice_id INT,
    due_date DATE
);

INSERT INTO Invoices VALUES
(1, '2026-11-20'),
(2, '2026-11-21'),
(3, '2026-11-24');

CREATE TABLE Public_Holidays (
    holiday_date DATE
);

INSERT INTO Public_Holidays VALUES
('2026-11-23');
```

---

## Day 147 – Calculate Percent Change From Previous Non-Zero Month (Window Functions)
**Table:** `Monthly_Exports`  
**Columns:** `export_month`, `export_value`  

Write a query to compute the percentage growth in `export_value` compared to the most recent prior month that had a strictly positive (`> 0`) export value, skipping over `0` months.

```sql
CREATE TABLE Monthly_Exports (
    export_month DATE,
    export_value DECIMAL(10, 2)
);

INSERT INTO Monthly_Exports VALUES
('2026-07-01', 20000.00),
('2026-08-01', 0.00),
('2026-09-01', 0.00),
('2026-10-01', 25000.00),
('2026-11-01', 30000.00);
```

---

## Day 148 – Bridge Table Many-to-Many Join: Students Enrolled in All Required Courses (Joins)
**Table:** `Students`  
**Columns:** `student_id`, `student_name`  

**Table:** `Enrollments`  
**Columns:** `student_id`, `course_code`  

**Table:** `Required_Courses`  
**Columns:** `course_code`  

Write a query to find the names of students who have completed every single course listed in `Required_Courses` (even if they also took extra elective courses).

```sql
CREATE TABLE Students (
    student_id INT,
    student_name VARCHAR(50)
);

INSERT INTO Students VALUES (1, 'Riya'), (2, 'Kabir'), (3, 'Aryan');

CREATE TABLE Required_Courses (
    course_code VARCHAR(10)
);

INSERT INTO Required_Courses VALUES ('SQL101'), ('PY101');

CREATE TABLE Enrollments (
    student_id INT,
    course_code VARCHAR(10)
);

INSERT INTO Enrollments VALUES
(1, 'SQL101'), (1, 'PY101'), (1, 'ML201'),
(2, 'SQL101'),
(3, 'SQL101'), (3, 'PY101');
```

---

## Day 149 – Detect & Flag Outliers Using Interquartile Range (IQR) (Window Functions + Data Cleaning)
**Table:** `Delivery_Times`  
**Columns:** `delivery_id`, `minutes_taken`  

Write a query to calculate the 25th percentile ($Q1$), 75th percentile ($Q3$), and Interquartile Range ($IQR = Q3 - Q1$), and flag any delivery where `minutes_taken > Q3 + 1.5 * IQR` as an `'Outlier'`.

```sql
CREATE TABLE Delivery_Times (
    delivery_id INT,
    minutes_taken INT
);

INSERT INTO Delivery_Times VALUES
(1, 25), (2, 28), (3, 30), (4, 32),
(5, 35), (6, 36), (7, 40), (8, 95);
```

---

## Day 150 – Point-in-Time Employee Department & Salary Reconstruction (SCD Type 2 Join)
**Table:** `Employee_History`  
**Columns:** `emp_id`, `dept`, `salary`, `valid_from`, `valid_to`  

**Table:** `Audit_Dates`  
**Columns:** `audit_date`  

Write a query to reconstruct the exact department and salary of every active employee on each `audit_date` (`valid_to` is `NULL` for currently active records).

```sql
CREATE TABLE Employee_History (
    emp_id INT,
    dept VARCHAR(30),
    salary INT,
    valid_from DATE,
    valid_to DATE
);

INSERT INTO Employee_History VALUES
(101, 'Sales', 60000, '2026-01-01', '2026-06-30'),
(101, 'Marketing', 75000, '2026-07-01', NULL),
(102, 'Tech', 90000, '2026-03-01', '2026-09-30');

CREATE TABLE Audit_Dates (
    audit_date DATE
);

INSERT INTO Audit_Dates VALUES
('2026-05-15'),
('2026-10-15');
```