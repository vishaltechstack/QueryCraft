# SQL Practice Problems (Day 151 – Day 200)

A comprehensive collection of 50 advanced SQL problems covering **SCD Type 2 Compression, Window Functions, Complex Joins, Date/Time Calculations, and Data Cleaning**.

## Day 151 – Deduplicate Overlapping Address History (SCD Type 2 Compression)

**Table:** `Customer_Addresses`

**Columns:** `cust_id`, `city`, `start_date`, `end_date`

Write a query to merge consecutive address history rows for the same customer where the `city` did not change, returning the earliest `start_date` and latest `end_date` for each continuous stay.

```sql
CREATE TABLE Customer_Addresses (
    cust_id INT,
    city VARCHAR(50),
    start_date DATE,
    end_date DATE
);

INSERT INTO Customer_Addresses VALUES
(1, 'Delhi', '2025-01-01', '2025-06-30'),
(1, 'Delhi', '2025-07-01', '2025-12-31'),
(1, 'Mumbai', '2026-01-01', '2026-06-30'),
(1, 'Delhi', '2026-07-01', NULL);
```

## Day 152 – Calculate Customer Churn Rate by Signup Cohort (Date/Time + Joins)

**Table:** `Users`

**Columns:** `user_id`, `signup_date`, `churn_date`

Write a query to group users by their signup month (`YYYY-MM`) and calculate the percentage of users from each cohort who churned within 60 days of signing up (`churn_date` is `NULL` for active users).

```sql
CREATE TABLE Users (
    user_id INT,
    signup_date DATE,
    churn_date DATE
);

INSERT INTO Users VALUES
(1, '2026-08-05', '2026-09-10'),
(2, '2026-08-12', NULL),
(3, '2026-08-20', '2026-11-15'),
(4, '2026-09-02', '2026-10-01');
```

## Day 153 – Top-N Products Per Category Including Ties (DENSE_RANK vs. RANK)

**Table:** `Category_Sales`

**Columns:** `category`, `product_name`, `units_sold`

Write a query to retrieve all products that rank in the top 2 unique sales volumes within their category.

```sql
CREATE TABLE Category_Sales (
    category VARCHAR(30),
    product_name VARCHAR(50),
    units_sold INT
);

INSERT INTO Category_Sales VALUES
('Audio', 'Earbuds Pro', 500),
('Audio', 'Headphones X', 500),
('Audio', 'Speaker Mini', 350),
('Audio', 'Soundbar', 200);
```

## Day 154 – Extract & Validate PAN Card Format (Data Cleaning)

**Table:** `KYC_Records`

**Columns:** `applicant_id`, `raw_pan`

Write a query to clean `raw_pan` (trim spaces, convert to uppercase) and validate whether it matches the standard Indian PAN format (`5 uppercase letters + 4 digits + 1 uppercase letter`), returning `'Valid'` or `'Invalid'`.

```sql
CREATE TABLE KYC_Records (
    applicant_id INT,
    raw_pan VARCHAR(20)
);

INSERT INTO KYC_Records VALUES
(1, '  abcde1234f '),
(2, 'ABCDE12345'),
(3, 'XYZPQ9876K'),
(4, '12345ABCDE');
```

## Day 155 – Self Join: Find Employees Earning More Than Both Their Manager and Grand-Manager (Joins)

**Table:** `Corp_Employees`

**Columns:** `emp_id`, `emp_name`, `salary`, `manager_id`

Write a query to find employees whose salary is strictly higher than their direct manager's salary AND their manager's manager's salary.

```sql
CREATE TABLE Corp_Employees (
    emp_id INT,
    emp_name VARCHAR(50),
    salary INT,
    manager_id INT
);

INSERT INTO Corp_Employees VALUES
(1, 'Director', 150000, NULL),
(2, 'Manager', 120000, 1),
(3, 'Senior Dev', 160000, 2),
(4, 'Junior Dev', 90000, 3);
```

## Day 156 – Calculate Session Timeout & Idle Duration Between Clicks (Date/Time + Window Functions)

**Table:** `App_Clicks`

**Columns:** `user_id`, `screen_name`, `click_ts`

Write a query to calculate the time spent (in seconds) on each screen before navigating to the next screen, setting the duration of the final screen in a day to `NULL`.

```sql
CREATE TABLE App_Clicks (
    user_id INT,
    screen_name VARCHAR(30),
    click_ts TIMESTAMP
);

INSERT INTO App_Clicks VALUES
(1, 'Splash', '2026-11-24 09:00:00'),
(1, 'Feed', '2026-11-24 09:00:12'),
(1, 'Profile', '2026-11-24 09:02:45'),
(1, 'Settings', '2026-11-24 09:03:10');
```

## Day 157 – Reconcile Split Payments Against Invoice Totals (Joins)

**Table:** `Customer_Invoices`

**Columns:** `invoice_id`, `billed_amount`

**Table:** `Payment_Installments`

**Columns:** `payment_id`, `invoice_id`, `paid_amount`

Write a query to classify each invoice as `'Paid'`, `'Partially Paid'`, or `'Unpaid'` by comparing total received installments against `billed_amount`.

```sql
CREATE TABLE Customer_Invoices (
    invoice_id INT,
    billed_amount DECIMAL(10, 2)
);

INSERT INTO Customer_Invoices VALUES (1, 1000.00), (2, 1500.00), (3, 800.00);

CREATE TABLE Payment_Installments (
    payment_id INT,
    invoice_id INT,
    paid_amount DECIMAL(10, 2)
);

INSERT INTO Payment_Installments VALUES
(10, 1, 600.00),
(11, 1, 400.00),
(12, 2, 500.00);
```

## Day 158 – Normalize Unstructured Delimited Key-Value Logs (Data Cleaning)

**Table:** `Server_Logs`

**Columns:** `log_id`, `raw_log`

Write a query to parse the pipe-delimited `raw_log` string into separate `status_code`, `latency_ms`, and `endpoint` columns.

```sql
CREATE TABLE Server_Logs (
    log_id INT,
    raw_log VARCHAR(150)
);

INSERT INTO Server_Logs VALUES
(1, 'status=200|latency=45ms|endpoint=/api/v1/users'),
(2, 'status=500|latency=1200ms|endpoint=/api/v1/checkout');
```

## Day 159 – Find Peak 15-Minute Sliding Window Order Volume (Date/Time + Window Functions)

**Table:** `Food_Orders`

**Columns:** `order_id`, `order_time`

Write a query to find the maximum number of orders placed within any 15-minute rolling interval (`RANGE BETWEEN INTERVAL '15 minutes' PRECEDING AND CURRENT ROW`).

```sql
CREATE TABLE Food_Orders (
    order_id INT,
    order_time TIMESTAMP
);

INSERT INTO Food_Orders VALUES
(1, '2026-11-24 19:00:00'),
(2, '2026-11-24 19:05:00'),
(3, '2026-11-24 19:12:00'),
(4, '2026-11-24 19:14:00'),
(5, '2026-11-24 19:35:00');
```

## Day 160 – Bidirectional Friend Recommendations (People You May Know) (Joins)

**Table:** `User_Connections`

**Columns:** `user_a`, `user_b`

Write a query to recommend pairs of users who are **not** currently friends with each other, ranked by the highest number of mutual friends.

```sql
CREATE TABLE User_Connections (
    user_a INT,
    user_b INT
);

INSERT INTO User_Connections VALUES
(1, 2), (1, 3),
(2, 4), (3, 4),
(2, 5);
```

## Day 161 – Forward Fill Missing Categorical Values Within Partitions (Window Functions + Data Cleaning)

**Table:** `Device_Status_Log`

**Columns:** `device_id`, `log_time`, `firmware_version`

Write a query to replace `NULL` entries in `firmware_version` with the last known non-null version for that specific `device_id`.

```sql
CREATE TABLE Device_Status_Log (
    device_id INT,
    log_time TIMESTAMP,
    firmware_version VARCHAR(20)
);

INSERT INTO Device_Status_Log VALUES
(1, '2026-11-24 08:00:00', 'v1.0.2'),
(1, '2026-11-24 09:00:00', NULL),
(1, '2026-11-24 10:00:00', 'v1.1.0'),
(2, '2026-11-24 08:00:00', 'v2.0.0'),
(2, '2026-11-24 09:00:00', NULL);
```

## Day 162 – Calculate Prorated Monthly Subscription Revenue (Date/Time)

**Table:** `MidMonth_Plans`

**Columns:** `sub_id`, `start_date`, `monthly_price`

Write a query to calculate the exact prorated revenue earned in `'2026-11'` (a 30-day month) for subscriptions that started mid-month, inclusive of `start_date`.

```sql
CREATE TABLE MidMonth_Plans (
    sub_id INT,
    start_date DATE,
    monthly_price DECIMAL(10, 2)
);

INSERT INTO MidMonth_Plans VALUES
(1, '2026-11-01', 3000.00),
(2, '2026-11-16', 3000.00),
(3, '2026-11-25', 1500.00);
```

## Day 163 – Identify Customers Whose Order Spend Strictly Increased Every Consecutive Order (Window Functions)

**Table:** `Order_Progression`

**Columns:** `cust_id`, `order_date`, `amount`

Write a query to find customers with at least 3 orders whose order `amount` strictly increased (`current > previous`) on every single subsequent order.

```sql
CREATE TABLE Order_Progression (
    cust_id INT,
    order_date DATE,
    amount INT
);

INSERT INTO Order_Progression VALUES
(1, '2026-09-01', 100), (1, '2026-10-01', 250), (1, '2026-11-01', 400),
(2, '2026-09-01', 300), (2, '2026-10-01', 200), (2, '2026-11-01', 500),
(3, '2026-10-01', 150), (3, '2026-11-01', 300);
```

## Day 164 – Strip Repeated Words & Extra Internal Whitespace (Data Cleaning)

**Table:** `Dirty_Titles`

**Columns:** `doc_id`, `raw_title`

Write a query to collapse multiple consecutive spaces into a single space and trim leading/trailing spaces from `raw_title`.

```sql
CREATE TABLE Dirty_Titles (
    doc_id INT,
    raw_title VARCHAR(100)
);

INSERT INTO Dirty_Titles VALUES
(1, '   Annual    Financial     Report   2026  '),
(2, 'Q3   Sales      Summary');
```

## Day 165 – Multi-Hop Flight Connections (Exactly One Stop) (Self Join)

**Table:** `Direct_Flights`

**Columns:** `flight_id`, `origin`, `dest`, `dep_time`, `arr_time`, `price`

Write a query to find all valid one-stop flight itineraries from `'Delhi'` to `'Bengaluru'` where the layover time between the first flight's arrival and the second flight's departure is between 1 hour and 4 hours.

```sql
CREATE TABLE Direct_Flights (
    flight_id VARCHAR(10),
    origin VARCHAR(30),
    dest VARCHAR(30),
    dep_time TIMESTAMP,
    arr_time TIMESTAMP,
    price INT
);

INSERT INTO Direct_Flights VALUES
('AI101', 'Delhi', 'Mumbai', '2026-11-25 08:00:00', '2026-11-25 10:00:00', 4500),
('AI202', 'Mumbai', 'Bengaluru', '2026-11-25 11:30:00', '2026-11-25 13:15:00', 3500),
('AI203', 'Mumbai', 'Bengaluru', '2026-11-25 10:20:00', '2026-11-25 12:00:00', 3000);
```

## Day 166 – Calculate Drawdown & Maximum Peak-to-Trough Drop (Window Functions)

**Table:** `Fund_NAV`

**Columns:** `nav_date`, `nav_value`

Write a query to compute the running peak `nav_value` up to each date, the daily percentage drawdown from that peak, and the maximum drawdown across the entire period.

```sql
CREATE TABLE Fund_NAV (
    nav_date DATE,
    nav_value DECIMAL(10, 2)
);

INSERT INTO Fund_NAV VALUES
('2026-11-01', 100.00),
('2026-11-02', 120.00),
('2026-11-03', 90.00),
('2026-11-04', 110.00),
('2026-11-05', 130.00);
```

## Day 167 – Group Events into Weekly Buckets Starting Monday (Date/Time)

**Table:** `Site_Visits`

**Columns:** `visit_id`, `visit_time`

Write a query to truncate each `visit_time` to the Monday of its respective week (`week_start_date`) and count total visits per week.

```sql
CREATE TABLE Site_Visits (
    visit_id INT,
    visit_time TIMESTAMP
);

INSERT INTO Site_Visits VALUES
(1, '2026-11-18 14:20:00'),
(2, '2026-11-22 19:00:00'),
(3, '2026-11-23 08:30:00'),
(4, '2026-11-25 11:15:00');
```

## Day 168 – Pivot Variable Attributes Using Dynamic-Style Conditional Aggregation (Data Cleaning)

**Table:** `Entity_Attributes`

**Columns:** `entity_id`, `attr_name`, `attr_value`

Write a query to transform the Entity-Attribute-Value (EAV) table into a flat relational table with columns `entity_id`, `brand`, `warranty_months`, and `weight_kg`.

```sql
CREATE TABLE Entity_Attributes (
    entity_id INT,
    attr_name VARCHAR(30),
    attr_value VARCHAR(50)
);

INSERT INTO Entity_Attributes VALUES
(1, 'brand', 'Sony'),
(1, 'warranty_months', '24'),
(2, 'brand', 'LG'),
(2, 'weight_kg', '12.5');
```

## Day 169 – Match Nearest Geographic Store Within Same City (Joins + Window Functions)

**Table:** `Customer_Coords`

**Columns:** `cust_id`, `city`, `lat`, `lon`

**Table:** `Store_Coords`

**Columns:** `store_id`, `city`, `lat`, `lon`

Write a query to find the single closest store for each customer in the same city using Euclidean distance approximation $\sqrt{(lat_1 - lat_2)^2 + (lon_1 - lon_2)^2}$.

```sql
CREATE TABLE Customer_Coords (
    cust_id INT,
    city VARCHAR(30),
    lat DECIMAL(8, 4),
    lon DECIMAL(8, 4)
);

INSERT INTO Customer_Coords VALUES (1, 'Delhi', 28.6139, 77.2090);

CREATE TABLE Store_Coords (
    store_id INT,
    city VARCHAR(30),
    lat DECIMAL(8, 4),
    lon DECIMAL(8, 4)
);

INSERT INTO Store_Coords VALUES
(101, 'Delhi', 28.5355, 77.3910),
(102, 'Delhi', 28.6304, 77.2177);
```

## Day 170 – Calculate Win/Loss Streaks in Sports Matches (Window Functions)

**Table:** `Match_Results`

**Columns:** `match_date`, `team`, `result`

Write a query to determine each team's longest consecutive winning streak (`result = 'W'`).

```sql
CREATE TABLE Match_Results (
    match_date DATE,
    team VARCHAR(30),
    result CHAR(1)
);

INSERT INTO Match_Results VALUES
('2026-10-01', 'India', 'W'),
('2026-10-05', 'India', 'W'),
('2026-10-10', 'India', 'L'),
('2026-10-15', 'India', 'W'),
('2026-10-20', 'India', 'W'),
('2026-10-25', 'India', 'W');
```

## Day 171 – Reconstruct Hierarchical Breadcrumb Path (Recursive CTE)

**Table:** `Category_Tree`

**Columns:** `cat_id`, `cat_name`, `parent_id`

Write a query using a Recursive CTE to generate the full category path string (e.g., `'Electronics > Computers > Laptops'`) for every node in the tree.

```sql
CREATE TABLE Category_Tree (
    cat_id INT,
    cat_name VARCHAR(40),
    parent_id INT
);

INSERT INTO Category_Tree VALUES
(1, 'Electronics', NULL),
(2, 'Computers', 1),
(3, 'Laptops', 2),
(4, 'Smartphones', 1);
```

## Day 172 – Parse & Convert ISO 8601 Duration Strings to Seconds (Data Cleaning + Date/Time)

**Table:** `Video_Metrics`

**Columns:** `video_id`, `duration_str`

Write a query to parse duration strings formatted as `'HH:MM:SS'` or `'MM:SS'` into total integer seconds.

```sql
CREATE TABLE Video_Metrics (
    video_id INT,
    duration_str VARCHAR(15)
);

INSERT INTO Video_Metrics VALUES
(1, '01:15:30'),
(2, '08:45'),
(3, '00:02:10');
```

## Day 173 – Identify Churn Risk: Users Whose Weekly Activity Dropped by >50% (Window Functions + Date/Time)

**Table:** `Weekly_Usage`

**Columns:** `user_id`, `week_start`, `minutes_active`

Write a query to flag users whose `minutes_active` in any week dropped by more than 50% compared to their previous active week.

```sql
CREATE TABLE Weekly_Usage (
    user_id INT,
    week_start DATE,
    minutes_active INT
);

INSERT INTO Weekly_Usage VALUES
(1, '2026-11-02', 200),
(1, '2026-11-09', 180),
(1, '2026-11-16', 70),
(2, '2026-11-09', 100),
(2, '2026-11-16', 80);
```

## Day 174 – Cross-Database Schema Drift Detection (Joins + Data Cleaning)

**Table:** `Prod_Schema`

**Columns:** `table_name`, `column_name`, `data_type`

**Table:** `Staging_Schema`

**Columns:** `table_name`, `column_name`, `data_type`

Write a query to detect schema drift between Staging and Production, flagging columns that were `'Added in Staging'`, `'Missing in Staging'`, or `'Data Type Mismatch'`.

```sql
CREATE TABLE Prod_Schema (
    table_name VARCHAR(30),
    column_name VARCHAR(30),
    data_type VARCHAR(20)
);

INSERT INTO Prod_Schema VALUES
('orders', 'id', 'INT'),
('orders', 'amount', 'DECIMAL(10,2)'),
('orders', 'legacy_flag', 'CHAR(1)');

CREATE TABLE Staging_Schema (
    table_name VARCHAR(30),
    column_name VARCHAR(30),
    data_type VARCHAR(20)
);

INSERT INTO Staging_Schema VALUES
('orders', 'id', 'BIGINT'),
('orders', 'amount', 'DECIMAL(10,2)'),
('orders', 'coupon_code', 'VARCHAR(20)');
```

## Day 175 – Calculate First-Order vs. Repeat-Order Revenue Split Per Month (Window Functions + Date/Time)

**Table:** `Ecommerce_Txns`

**Columns:** `txn_id`, `user_id`, `txn_date`, `revenue`

Write a query to calculate the monthly revenue split into `new_customer_revenue` (from a user's very first order) and `repeat_customer_revenue` (from subsequent orders).

```sql
CREATE TABLE Ecommerce_Txns (
    txn_id INT,
    user_id INT,
    txn_date DATE,
    revenue INT
);

INSERT INTO Ecommerce_Txns VALUES
(1, 10, '2026-10-05', 500),
(2, 10, '2026-11-10', 800),
(3, 20, '2026-11-12', 600);
```

## Day 176 – Clean & Standardize International Phone Country Codes (Data Cleaning)

**Table:** `Global_Leads`

**Columns:** `lead_id`, `phone_raw`

Write a query to extract the country code (`'+91'`, `'+1'`, `'+44'`) and the 10-digit subscriber number separately, defaulting to `'+91'` if no country prefix is present.

```sql
CREATE TABLE Global_Leads (
    lead_id INT,
    phone_raw VARCHAR(25)
);

INSERT INTO Global_Leads VALUES
(1, '+91-9876543210'),
(2, '9876543211'),
(3, '+1 (415) 555-0199'),
(4, '0044-7700900077');
```

## Day 177 – Find Median Time to First Purchase After Registration (Date/Time + Joins + Window Functions)

**Table:** `Registrations`

**Columns:** `user_id`, `reg_time`

**Table:** `First_Orders`

**Columns:** `user_id`, `order_time`

Write a query to compute the median number of hours elapsed between registration and a user's first purchase (excluding users who never purchased).

```sql
CREATE TABLE Registrations (
    user_id INT,
    reg_time TIMESTAMP
);

INSERT INTO Registrations VALUES
(1, '2026-11-20 10:00:00'),
(2, '2026-11-20 12:00:00'),
(3, '2026-11-21 09:00:00'),
(4, '2026-11-21 15:00:00');

CREATE TABLE First_Orders (
    user_id INT,
    order_time TIMESTAMP
);

INSERT INTO First_Orders VALUES
(1, '2026-11-20 12:00:00'),
(2, '2026-11-21 00:00:00'),
(3, '2026-11-23 09:00:00');
```

## Day 178 – Allocate Fixed Overhead Costs Proportionally by Revenue (Window Functions)

**Table:** `Branch_Revenue`

**Columns:** `branch_name`, `revenue`

Write a query to allocate a fixed shared corporate cost of `₹1,00,000` across branches proportionally based on their share of total revenue, ensuring the allocated amounts are rounded to 2 decimal places.

```sql
CREATE TABLE Branch_Revenue (
    branch_name VARCHAR(30),
    revenue INT
);

INSERT INTO Branch_Revenue VALUES
('North', 500000),
('South', 300000),
('West', 200000);
```

## Day 179 – Detect Duplicate Records Using Fuzzy Soundex / Phonetic Similarity (Data Cleaning + Self Join)

**Table:** `Customer_Names`

**Columns:** `cust_id`, `full_name`

Write a query using `SOUNDEX()` (or normalized consonant matching) to find pairs of customer records that sound identical despite minor spelling variations.

```sql
CREATE TABLE Customer_Names (
    cust_id INT,
    full_name VARCHAR(50)
);

INSERT INTO Customer_Names VALUES
(1, 'Saurabh'),
(2, 'Sourav'),
(3, 'Abhishek'),
(4, 'Abishek');
```

## Day 180 – Identify Concurrent Seat Bookings Overbooking Conflicts (Self Join + Date/Time)

**Table:** `Room_Reservations`

**Columns:** `res_id`, `room_no`, `check_in`, `check_out`

Write a query to detect any pair of reservations for the same `room_no` where the stay dates overlap (`check_in_1 < check_out_2` AND `check_in_2 < check_out_1`).

```sql
CREATE TABLE Room_Reservations (
    res_id INT,
    room_no INT,
    check_in DATE,
    check_out DATE
);

INSERT INTO Room_Reservations VALUES
(1, 101, '2026-12-01', '2026-12-05'),
(2, 101, '2026-12-04', '2026-12-07'),
(3, 101, '2026-12-07', '2026-12-10');
```

## Day 181 – Calculate Rolling 4-Quarter YoY Revenue Growth (Window Functions + Date/Time)

**Table:** `Quarterly_Earnings`

**Columns:** `yr`, `qtr`, `revenue`

Write a query to compare each quarter's revenue against the exact same quarter in the previous year (`LAG(revenue, 4)`) and compute the YoY percentage change.

```sql
CREATE TABLE Quarterly_Earnings (
    yr INT,
    qtr INT,
    revenue INT
);

INSERT INTO Quarterly_Earnings VALUES
(2025, 1, 100), (2025, 2, 120), (2025, 3, 110), (2025, 4, 150),
(2026, 1, 125), (2026, 2, 132);
```

## Day 182 – Clean & Split Semicolon-Separated Emails with Validation (Data Cleaning)

**Table:** `Bulk_Contacts`

**Columns:** `group_id`, `email_list`

Write a query to split `email_list` into individual rows, trim whitespace, lowercase the text, and filter out any malformed strings that do not contain `@` and `.`.

```sql
CREATE TABLE Bulk_Contacts (
    group_id INT,
    email_list VARCHAR(200)
);

INSERT INTO Bulk_Contacts VALUES
(1, 'Amit@Gmail.com; invalid-email ; Neha@Yahoo.co.in '),
(2, 'rohan@company.com; test@');
```

## Day 183 – Find Longest Active Streak of Daily App Opens Allowing 1-Day Grace Gap (Window Functions + Date/Time)

**Table:** `App_Opens`

**Columns:** `user_id`, `open_date`

Write a query to find each user's longest streak of app opens where a gap of up to 1 missed day (`open_date - prev_date <= 2`) still continues the streak.

```sql
CREATE TABLE App_Opens (
    user_id INT,
    open_date DATE
);

INSERT INTO App_Opens VALUES
(1, '2026-11-01'),
(1, '2026-11-02'),
(1, '2026-11-04'),
(1, '2026-11-05'),
(1, '2026-11-09');
```

## Day 184 – Anti-Join Across Composite Keys: Unfulfilled Line Items (Joins)

**Table:** `Sales_Order_Items`

**Columns:** `order_id`, `sku`, `ordered_qty`

**Table:** `Shipment_Items`

**Columns:** `order_id`, `sku`, `shipped_qty`

Write a query to find all `(order_id, sku)` combinations that either have not been shipped at all or have a `shipped_qty` less than `ordered_qty`.

```sql
CREATE TABLE Sales_Order_Items (
    order_id INT,
    sku VARCHAR(20),
    ordered_qty INT
);

INSERT INTO Sales_Order_Items VALUES
(1, 'SKU-A', 10),
(1, 'SKU-B', 5),
(2, 'SKU-C', 8);

CREATE TABLE Shipment_Items (
    order_id INT,
    sku VARCHAR(20),
    shipped_qty INT
);

INSERT INTO Shipment_Items VALUES
(1, 'SKU-A', 10),
(1, 'SKU-B', 3);
```

## Day 185 – Calculate Customer Recency, Frequency, and Monetary (RFM) Scores (Window Functions + Date/Time)

**Table:** `Retail_Txns`

**Columns:** `cust_id`, `txn_date`, `spend`

Write a query as of `'2026-11-25'` to compute each customer's Recency (days since last purchase), Frequency (total orders), Monetary (total spend), and assign `NTILE(3)` scores (`1` to `3`) for each metric.

```sql
CREATE TABLE Retail_Txns (
    cust_id INT,
    txn_date DATE,
    spend INT
);

INSERT INTO Retail_Txns VALUES
(1, '2026-11-20', 5000), (1, '2026-11-24', 3000),
(2, '2026-10-01', 1500),
(3, '2026-11-10', 4000), (3, '2026-11-15', 4500), (3, '2026-11-22', 2000);
```

## Day 186 – Normalize Roman Numerals & Suffixes in Person Names (Data Cleaning)

**Table:** `Client_Registry`

**Columns:** `client_id`, `raw_name`

Write a query to strip common prefixes (`Mr.`, `Mrs.`, `Dr.`) and suffixes (`Jr.`, `Sr.`, `III`) from `raw_name` to extract the clean core name.

```sql
CREATE TABLE Client_Registry (
    client_id INT,
    raw_name VARCHAR(60)
);

INSERT INTO Client_Registry VALUES
(1, 'Dr. Rajesh Khanna'),
(2, 'Mr. Vikramaditya Roy Jr.'),
(3, 'Mrs. Sunita Sharma');
```

## Day 187 – Calculate Time-to-Resolution Percentiles (P50, P90, P99) by Priority (Window Functions + Date/Time)

**Table:** `Incident_Logs`

**Columns:** `incident_id`, `priority`, `created_ts`, `resolved_ts`

Write a query to compute the P50 (median) and P90 resolution times in minutes grouped by ticket `priority`.

```sql
CREATE TABLE Incident_Logs (
    incident_id INT,
    priority VARCHAR(10),
    created_ts TIMESTAMP,
    resolved_ts TIMESTAMP
);

INSERT INTO Incident_Logs VALUES
(1, 'P1', '2026-11-24 08:00:00', '2026-11-24 08:20:00'),
(2, 'P1', '2026-11-24 09:00:00', '2026-11-24 09:40:00'),
(3, 'P1', '2026-11-24 10:00:00', '2026-11-24 12:00:00'),
(4, 'P2', '2026-11-24 08:00:00', '2026-11-24 11:00:00');
```

## Day 188 – Bridge Table Rollup: Revenue Attribution Across Multiple Sales Reps (Joins)

**Table:** `Deals`

**Columns:** `deal_id`, `deal_value`

**Table:** `Deal_Splits`

**Columns:** `deal_id`, `rep_name`, `split_pct`

Write a query to calculate each sales rep's total attributed revenue based on their percentage split on closed deals.

```sql
CREATE TABLE Deals (
    deal_id INT,
    deal_value DECIMAL(10, 2)
);

INSERT INTO Deals VALUES (101, 100000.00), (102, 50000.00);

CREATE TABLE Deal_Splits (
    deal_id INT,
    rep_name VARCHAR(40),
    split_pct DECIMAL(5, 2)
);

INSERT INTO Deal_Splits VALUES
(101, 'Aarav', 0.60),
(101, 'Diya', 0.40),
(102, 'Diya', 1.00);
```

## Day 189 – Detect & Remove Corrupted Non-ASCII Characters (Data Cleaning)

**Table:** `Product_Catalog`

**Columns:** `prod_id`, `raw_title`

Write a query to clean `raw_title` by removing any non-ASCII / special mojibake characters while preserving standard alphanumeric characters, spaces, and hyphens.

```sql
CREATE TABLE Product_Catalog (
    prod_id INT,
    raw_title VARCHAR(100)
);

INSERT INTO Product_Catalog VALUES
(1, 'Wireless Mouse â€“ Black'),
(2, 'USB-C Hub™ 7-in-1');
```

## Day 190 – Calculate Net Retention Rate (NRR) Including Expansion & Contraction (Joins + Date/Time)

**Table:** `MRR_Snapshots`

**Columns:** `cust_id`, `snap_month`, `mrr`

Write a query to calculate the Net Revenue Retention (NRR) percentage from `'2026-10-01'` to `'2026-11-01'` for existing October customers ($\frac{\text{November MRR of Oct Cohort}}{\text{Total October MRR}} \times 100$).

```sql
CREATE TABLE MRR_Snapshots (
    cust_id INT,
    snap_month DATE,
    mrr INT
);

INSERT INTO MRR_Snapshots VALUES
(1, '2026-10-01', 1000), (1, '2026-11-01', 1500),
(2, '2026-10-01', 1000), (2, '2026-11-01', 0),
(3, '2026-11-01', 2000);
```

## Day 191 – Find First Day Each Product Stock Dropped Below Reorder Threshold (Window Functions)

**Table:** `Daily_Stock`

**Columns:** `sku`, `stock_date`, `closing_qty`

Write a query to find the earliest `stock_date` on which each `sku` dropped below `20` units after having previously been at or above `20` units.

```sql
CREATE TABLE Daily_Stock (
    sku VARCHAR(20),
    stock_date DATE,
    closing_qty INT
);

INSERT INTO Daily_Stock VALUES
('SKU-1', '2026-11-20', 50),
('SKU-1', '2026-11-21', 25),
('SKU-1', '2026-11-22', 18),
('SKU-1', '2026-11-23', 12);
```

## Day 192 – Generate Hourly Time-Series Heatmap Filling Zero-Activity Hours (Date/Time + Cross Join)

**Table:** `API_Calls`

**Columns:** `call_id`, `call_time`

Write a query to report the total number of API calls for every hour from `00:00` to `23:00` on `'2026-11-24'`, displaying `0` for hours with zero traffic.

```sql
CREATE TABLE API_Calls (
    call_id INT,
    call_time TIMESTAMP
);

INSERT INTO API_Calls VALUES
(1, '2026-11-24 02:15:00'),
(2, '2026-11-24 02:45:00'),
(3, '2026-11-24 14:10:00');
```

## Day 193 – Standardize Messy Boolean Survey Responses & Calculate NPS (Data Cleaning)

**Table:** `NPS_Responses`

**Columns:** `resp_id`, `raw_score`

Write a query to clean `raw_score` (extract numeric values from strings like `'10 - Extremely Likely'` or `' 8 '`, ignoring invalid text like `'N/A'`) and calculate the Net Promoter Score (`% Promoters [9-10] - % Detractors [0-6]`).

```sql
CREATE TABLE NPS_Responses (
    resp_id INT,
    raw_score VARCHAR(40)
);

INSERT INTO NPS_Responses VALUES
(1, '10 - Extremely Likely'),
(2, '  9 '),
(3, '7'),
(4, '4 - Poor'),
(5, 'N/A');
```

## Day 194 – Self Join: Detect Price Arbitrage Across Warehouses (Joins)

**Table:** `Warehouse_Prices`

**Columns:** `sku`, `warehouse`, `unit_price`

Write a query to find all SKUs where the price difference between the most expensive warehouse and the cheapest warehouse exceeds 25% of the cheapest price.

```sql
CREATE TABLE Warehouse_Prices (
    sku VARCHAR(20),
    warehouse VARCHAR(30),
    unit_price DECIMAL(10, 2)
);

INSERT INTO Warehouse_Prices VALUES
('ITEM-1', 'Delhi', 100.00),
('ITEM-1', 'Mumbai', 135.00),
('ITEM-2', 'Delhi', 200.00),
('ITEM-2', 'Chennai', 220.00);
```

## Day 195 – Calculate Rolling 7-Day Median & IQR Band for Anomaly Detection (Window Functions)

**Table:** `Checkout_Latency`

**Columns:** `log_date`, `p95_ms`

Write a query to compute the trailing 7-day average and standard deviation (excluding the current day) to flag days where `p95_ms` exceeded `avg + 3 * stddev`.

```sql
CREATE TABLE Checkout_Latency (
    log_date DATE,
    p95_ms INT
);

INSERT INTO Checkout_Latency VALUES
('2026-11-17', 120), ('2026-11-18', 125), ('2026-11-19', 118),
('2026-11-20', 122), ('2026-11-21', 121), ('2026-11-22', 119),
('2026-11-23', 124), ('2026-11-24', 480);
```

## Day 196 – Reconstruct Account Balance History Backwards from Current Balance (Window Functions)

**Table:** `Current_Balances`

**Columns:** `account_id`, `current_balance`

**Table:** `Recent_Txns`

**Columns:** `txn_id`, `account_id`, `txn_date`, `signed_amount`

Write a query to reconstruct the end-of-day balance for each prior transaction date by working backwards from `current_balance`.

```sql
CREATE TABLE Current_Balances (
    account_id INT,
    current_balance DECIMAL(10, 2)
);

INSERT INTO Current_Balances VALUES (101, 5000.00);

CREATE TABLE Recent_Txns (
    txn_id INT,
    account_id INT,
    txn_date DATE,
    signed_amount DECIMAL(10, 2)
);

INSERT INTO Recent_Txns VALUES
(1, 101, '2026-11-22', 1000.00),
(2, 101, '2026-11-23', -500.00),
(3, 101, '2026-11-24', 1500.00);
```

## Day 197 – Parse & Normalize Nested JSON Objects with Fallback Keys (Data Cleaning)

**Table:** `Payment_Webhooks`

**Columns:** `event_id`, `payload`

Write a query to extract the transaction status from `payload`, checking `$.data.status` first and falling back to `$.status` if the nested key does not exist.

```sql
CREATE TABLE Payment_Webhooks (
    event_id INT,
    payload VARCHAR(200)
);

INSERT INTO Payment_Webhooks VALUES
(1, '{"data": {"status": "SUCCESS", "amount": 500}}'),
(2, '{"status": "FAILED", "reason": "timeout"}');
```

## Day 198 – Calculate Multi-Touch Linear Attribution Credit Per Channel (Window Functions + Joins)

**Table:** `Touchpoints`

**Columns:** `user_id`, `channel`, `touch_time`

**Table:** `Conversions`

**Columns:** `conv_id`, `user_id`, `conv_time`, `order_value`

Write a query to distribute each conversion's `order_value` equally across all marketing touchpoints that occurred for that user prior to `conv_time` (Linear Attribution).

```sql
CREATE TABLE Touchpoints (
    user_id INT,
    channel VARCHAR(30),
    touch_time TIMESTAMP
);

INSERT INTO Touchpoints VALUES
(1, 'Search', '2026-11-20 10:00:00'),
(1, 'Social', '2026-11-21 14:00:00'),
(1, 'Email', '2026-11-22 09:00:00');

CREATE TABLE Conversions (
    conv_id INT,
    user_id INT,
    conv_time TIMESTAMP,
    order_value DECIMAL(10, 2)
);

INSERT INTO Conversions VALUES
(501, 1, '2026-11-22 12:00:00', 3000.00);
```

## Day 199 – Identify Mutual Exclusivity Violations in User Roles (Joins + Data Cleaning)

**Table:** `User_Roles`

**Columns:** `user_id`, `role_name`

Write a query to detect Segregation of Duties (SoD) compliance violations by finding users who simultaneously hold both `'Approver'` and `'Submitter'` roles.

```sql
CREATE TABLE User_Roles (
    user_id INT,
    role_name VARCHAR(30)
);

INSERT INTO User_Roles VALUES
(1, 'Submitter'),
(1, 'Approver'),
(2, 'Submitter'),
(3, 'Approver'),
(3, 'Auditor');
```

## Day 200 – End-to-End SaaS Billing & Usage Overage Engine (Capstone Challenge)

**Table:** `Plans`

**Columns:** `plan_id`, `base_fee`, `included_api_calls`, `overage_rate_per_100`

**Table:** `Customer_Plans`

**Columns:** `cust_id`, `plan_id`

**Table:** `Monthly_API_Usage`

**Columns:** `cust_id`, `billing_month`, `total_calls`

Write a query to calculate each customer's final monthly bill (`base_fee + overage_charges`), where overage charges apply only to calls exceeding `included_api_calls`, billed in blocks of 100 calls rounded up (`CEIL`).

```sql
CREATE TABLE Plans (
    plan_id VARCHAR(20),
    base_fee DECIMAL(10, 2),
    included_api_calls INT,
    overage_rate_per_100 DECIMAL(10, 2)
);

INSERT INTO Plans VALUES
('Starter', 1000.00, 10000, 50.00),
('Growth', 5000.00, 100000, 30.00);

CREATE TABLE Customer_Plans (
    cust_id INT,
    plan_id VARCHAR(20)
);

INSERT INTO Customer_Plans VALUES (1, 'Starter'), (2, 'Growth');

CREATE TABLE Monthly_API_Usage (
    cust_id INT,
    billing_month DATE,
    total_calls INT
);

INSERT INTO Monthly_API_Usage VALUES
(1, '2026-11-01', 10250),
(2, '2026-11-01', 95000);
```