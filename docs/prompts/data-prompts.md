# Data Prompts

A collection of prompt templates for data analysis, SQL queries, database design, and data engineering tasks.

---

## SQL Queries

### 1. Generate SQL Query

**Purpose:** Create SQL queries from natural language requirements.

**Prompt:**
```
Write a SQL query for [DATABASE_TYPE]:

Requirements:
- Goal: [WHAT_YOU_WANT_TO_RETRIEVE]
- Tables: [TABLE_NAMES_AND_SCHEMAS]
- Conditions: [FILTERS_AND_CRITERIA]
- Output: [COLUMNS_NEEDED]
- Sorting: [ORDER_BY_REQUIREMENTS]
- Aggregation: [GROUP_BY/AGGREGATE_FUNCTIONS]
- Performance: [INDEX_CONSIDERATIONS]

Provide:
- SQL query (formatted and commented)
- Explanation of key parts
- Expected result structure
- Performance considerations
- Indexes needed for optimization

Use [POSTGRESQL/MYSQL/SQLSERVER/ORACLE] syntax.
```

**Example:**
```
Write a PostgreSQL query:

Requirements:
- Goal: Find top 10 customers by revenue in last 30 days
- Tables:
  - customers (id, name, email, created_at)
  - orders (id, customer_id, total_amount, order_date, status)
- Conditions:
  - Orders from last 30 days
  - Only completed orders (status = 'completed')
  - Exclude deleted customers
- Output: Customer name, email, total revenue, order count
- Sorting: By total revenue descending
- Aggregation: Sum of order totals, count of orders per customer

Query:
```sql
-- Top 10 customers by revenue in last 30 days
SELECT
    c.name AS customer_name,
    c.email AS customer_email,
    COUNT(o.id) AS order_count,
    SUM(o.total_amount) AS total_revenue
FROM
    customers c
    INNER JOIN orders o ON c.id = o.customer_id
WHERE
    o.order_date >= CURRENT_DATE - INTERVAL '30 days'
    AND o.status = 'completed'
    AND c.deleted_at IS NULL  -- Exclude deleted customers
GROUP BY
    c.id, c.name, c.email  -- Group by customer
HAVING
    COUNT(o.id) > 0  -- Ensure at least 1 order
ORDER BY
    total_revenue DESC  -- Highest revenue first
LIMIT 10;  -- Top 10 only
```

Explanation:
- INNER JOIN: Links customers to their orders
- WHERE: Filters to last 30 days, completed orders, active customers
- GROUP BY: Aggregates orders per customer
- HAVING: Optional filter (at least 1 order, though guaranteed by INNER JOIN)
- ORDER BY + LIMIT: Returns top 10 by revenue

Expected Result:
```
customer_name | customer_email      | order_count | total_revenue
John Doe      | john@example.com    | 15          | 12,459.50
Jane Smith    | jane@example.com    | 8           | 9,832.00
...
```

Performance:
- Index on orders(order_date, status) for WHERE clause
- Index on orders(customer_id) for JOIN
- Index on customers(deleted_at) if soft deletes used
- Consider materialized view if run frequently

Estimated rows: ~1000 orders scanned, returns 10 rows
Execution time: <50ms with indexes
```

---

### 2. Optimize SQL Query

**Purpose:** Improve performance of slow SQL queries.

**Prompt:**
```
Optimize this SQL query:
[SLOW_QUERY]

Context:
- Database: [TYPE_AND_VERSION]
- Current execution time: [DURATION]
- Target execution time: [GOAL]
- Table sizes: [ROW_COUNTS]
- Existing indexes: [INDEX_LIST]
- Query frequency: [HOW_OFTEN_RUN]

Analyze:
- Identify performance bottlenecks
- Explain why it's slow
- Suggest query rewrite
- Recommend indexes
- Consider alternative approaches (materialized views, caching, etc.)

Provide:
- Optimized query
- Index creation statements
- Before/after execution plan comparison
- Estimated improvement
```

**Example:**
```
Optimize this PostgreSQL query:

Slow Query:
```sql
SELECT p.*,
       (SELECT COUNT(*) FROM order_items oi WHERE oi.product_id = p.id) as order_count,
       (SELECT AVG(r.rating) FROM reviews r WHERE r.product_id = p.id) as avg_rating
FROM products p
WHERE p.category_id = 5
ORDER BY p.name;
```

Context:
- Database: PostgreSQL 14
- Current time: 3.5 seconds
- Target: <200ms
- Table sizes: products (50k), order_items (2M), reviews (500k)
- Existing indexes: products(id), order_items(id), reviews(id)
- Frequency: Every page load (high traffic)

Analysis:

Bottlenecks:
1. Correlated subqueries execute once per row (50k times)
2. No indexes on foreign keys (product_id)
3. Sequential scan on products for category_id
4. Unnecessary SELECT p.* (fetching all columns)

Why it's slow:
- Subqueries are O(n*m) complexity
- No index on product_id causes full table scans for each product
- category_id filter not indexed
- Fetching unused columns wastes I/O

Optimized Query:
```sql
SELECT
    p.id,
    p.name,
    p.category_id,
    p.price,
    COALESCE(oi_counts.order_count, 0) AS order_count,
    COALESCE(r_avg.avg_rating, 0) AS avg_rating
FROM
    products p
    LEFT JOIN (
        SELECT product_id, COUNT(*) AS order_count
        FROM order_items
        GROUP BY product_id
    ) oi_counts ON p.id = oi_counts.product_id
    LEFT JOIN (
        SELECT product_id, AVG(rating) AS avg_rating
        FROM reviews
        GROUP BY product_id
    ) r_avg ON p.id = r_avg.product_id
WHERE
    p.category_id = 5
ORDER BY
    p.name;
```

Indexes Needed:
```sql
-- Index for WHERE clause
CREATE INDEX idx_products_category_id ON products(category_id);

-- Index for JOIN on order_items
CREATE INDEX idx_order_items_product_id ON order_items(product_id);

-- Index for JOIN on reviews
CREATE INDEX idx_reviews_product_id ON reviews(product_id);

-- Optional: Covering index for products (if few columns needed)
CREATE INDEX idx_products_category_name ON products(category_id, name)
INCLUDE (id, price);
```

Execution Plan Comparison:

Before:
```
Seq Scan on products  (cost=0..150000 rows=1000)
  SubPlan 1
    Aggregate  (cost=50..52 rows=1)
      Seq Scan on order_items  (cost=0..50)
  SubPlan 2
    Aggregate  (cost=30..32 rows=1)
      Seq Scan on reviews  (cost=0..30)

Execution time: 3,500ms
```

After:
```
Hash Left Join  (cost=1500..2000 rows=1000)
  Index Scan on products using idx_products_category_id
  Hash Join
    HashAggregate on order_items
      Index Scan using idx_order_items_product_id
  Hash Join
    HashAggregate on reviews
      Index Scan using idx_reviews_product_id

Execution time: ~120ms
```

Improvements:
- Query rewrite: Subqueries → JOINs (executes once per table, not per row)
- Indexes: Enable index scans instead of sequential scans
- COALESCE: Handle NULL values from LEFT JOIN
- Covering index: Reduces I/O (optional, but recommended)

Estimated improvement: 97% faster (3500ms → 120ms)

Alternative Approaches:

1. Materialized View (if data doesn't change often):
```sql
CREATE MATERIALIZED VIEW product_stats AS
SELECT
    p.id,
    p.name,
    p.category_id,
    COUNT(oi.id) AS order_count,
    AVG(r.rating) AS avg_rating
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
LEFT JOIN reviews r ON p.id = r.product_id
GROUP BY p.id;

CREATE INDEX idx_product_stats_category ON product_stats(category_id);

-- Refresh periodically
REFRESH MATERIALIZED VIEW CONCURRENTLY product_stats;

-- Query becomes:
SELECT * FROM product_stats WHERE category_id = 5 ORDER BY name;
-- Execution time: <10ms
```

2. Application-level caching:
- Cache aggregated stats (order_count, avg_rating) in Redis
- TTL: 5 minutes
- Invalidate on new order/review
- Reduces DB load for high-traffic pages

3. Denormalization:
- Add order_count, avg_rating columns to products table
- Update via triggers or background job
- Trade-off: Stale data (eventual consistency) for speed

Recommendation:
- Immediate: Apply indexes (quick, safe, big improvement)
- Short-term: Rewrite query with JOINs
- Long-term: Consider materialized view + cache for hot data
```

---

### 3. Complex Query Design

**Purpose:** Design queries for complex analytical or reporting needs.

**Prompt:**
```
Design a complex SQL query for [ANALYSIS_GOAL]:

Analysis requirements:
- Business question: [QUESTION_TO_ANSWER]
- Data sources: [TABLES_INVOLVED]
- Time period: [DATE_RANGE]
- Dimensions: [GROUP_BY_DIMENSIONS]
- Metrics: [CALCULATED_METRICS]
- Filters: [CONDITIONS]
- Edge cases: [SPECIAL_HANDLING]

Include:
- Main query with CTEs for readability
- Subqueries or window functions if needed
- Handling of NULL values and edge cases
- Date/time logic
- Comments explaining business logic
- Expected output structure
- Performance considerations for large datasets

Use analytical SQL features (CTEs, window functions, etc.).
```

**Example:**
```
Design query: Customer Cohort Retention Analysis

Business Question:
"Show monthly retention rate for customer cohorts acquired each month in 2023.
How many customers from each cohort made purchases in subsequent months?"

Data:
- customers (id, email, created_at)
- orders (id, customer_id, order_date, total_amount)

Requirements:
- Cohorts: Group customers by signup month
- Retention: % of cohort that made purchases in each subsequent month
- Time period: Cohorts from Jan-Dec 2023, track for 12 months
- Dimensions: Cohort month, months since signup
- Metrics: Customer count, retention %
- Filters: Completed orders only, exclude test accounts
- Edge cases: Customers who never ordered, months with no signups

Query:
```sql
-- Customer Cohort Retention Analysis
-- Shows percentage of customers from each cohort who made purchases in subsequent months

WITH
-- 1. Define cohorts (customers grouped by signup month)
customer_cohorts AS (
    SELECT
        id AS customer_id,
        DATE_TRUNC('month', created_at) AS cohort_month,
        created_at
    FROM customers
    WHERE
        created_at >= '2023-01-01'
        AND created_at < '2024-01-01'
        AND email NOT LIKE '%test%'  -- Exclude test accounts
),

-- 2. Get first order date for each customer
first_orders AS (
    SELECT
        customer_id,
        MIN(DATE_TRUNC('month', order_date)) AS first_order_month
    FROM orders
    WHERE status = 'completed'
    GROUP BY customer_id
),

-- 3. Calculate months since signup for each customer's first order
cohort_activity AS (
    SELECT
        cc.cohort_month,
        cc.customer_id,
        EXTRACT(YEAR FROM AGE(fo.first_order_month, cc.cohort_month)) * 12 +
        EXTRACT(MONTH FROM AGE(fo.first_order_month, cc.cohort_month)) AS months_since_signup
    FROM customer_cohorts cc
    LEFT JOIN first_orders fo ON cc.customer_id = fo.customer_id
),

-- 4. Count cohort size and active customers per month
cohort_retention AS (
    SELECT
        cohort_month,
        COUNT(DISTINCT customer_id) AS cohort_size,
        months_since_signup,
        COUNT(DISTINCT CASE WHEN months_since_signup IS NOT NULL THEN customer_id END) AS active_customers
    FROM cohort_activity
    WHERE months_since_signup IS NULL OR months_since_signup <= 12  -- Track up to 12 months
    GROUP BY cohort_month, months_since_signup
),

-- 5. Calculate retention percentage
cohort_summary AS (
    SELECT
        cohort_month,
        cohort_size,
        months_since_signup,
        active_customers,
        ROUND(100.0 * active_customers / NULLIF(cohort_size, 0), 2) AS retention_rate
    FROM cohort_retention
    JOIN (
        -- Get total cohort size (month 0)
        SELECT cohort_month, cohort_size
        FROM cohort_retention
        WHERE months_since_signup = 0 OR months_since_signup IS NULL
    ) cohort_sizes USING (cohort_month)
)

-- 6. Final output: Pivot-like display
SELECT
    TO_CHAR(cohort_month, 'YYYY-MM') AS cohort,
    cohort_size,
    MAX(CASE WHEN months_since_signup = 0 THEN retention_rate END) AS month_0,
    MAX(CASE WHEN months_since_signup = 1 THEN retention_rate END) AS month_1,
    MAX(CASE WHEN months_since_signup = 2 THEN retention_rate END) AS month_2,
    MAX(CASE WHEN months_since_signup = 3 THEN retention_rate END) AS month_3,
    MAX(CASE WHEN months_since_signup = 4 THEN retention_rate END) AS month_4,
    MAX(CASE WHEN months_since_signup = 5 THEN retention_rate END) AS month_5,
    MAX(CASE WHEN months_since_signup = 6 THEN retention_rate END) AS month_6,
    MAX(CASE WHEN months_since_signup = 7 THEN retention_rate END) AS month_7,
    MAX(CASE WHEN months_since_signup = 8 THEN retention_rate END) AS month_8,
    MAX(CASE WHEN months_since_signup = 9 THEN retention_rate END) AS month_9,
    MAX(CASE WHEN months_since_signup = 10 THEN retention_rate END) AS month_10,
    MAX(CASE WHEN months_since_signup = 11 THEN retention_rate END) AS month_11,
    MAX(CASE WHEN months_since_signup = 12 THEN retention_rate END) AS month_12
FROM cohort_summary
GROUP BY cohort_month, cohort_size
ORDER BY cohort_month;
```

Expected Output:
```
cohort   | cohort_size | month_0 | month_1 | month_2 | month_3 | ...
2023-01  | 1,250       | 100.00  | 45.60   | 38.40   | 32.80   | ...
2023-02  | 1,380       | 100.00  | 48.20   | 40.10   | 34.50   | ...
2023-03  | 1,520       | 100.00  | 46.70   | 39.20   | NULL    | ...
...
```

Business Logic Explained:
- Cohort: Customers grouped by month they signed up
- Month 0: Always 100% (all customers exist at signup)
- Month 1: % who made first purchase within 1 month of signup
- Month 2+: % who made first purchase within N months
- NULL: Not enough time has passed (e.g., Dec 2023 cohort can't have month 12)

Edge Cases Handled:
- Customers who never ordered: Included in cohort_size, reduce retention %
- Months with no signups: Not in result (no rows)
- Test accounts: Filtered out in customer_cohorts CTE
- NULL months_since_signup: Treated as 0 in aggregation

Performance Considerations:
- CTEs improve readability but may not optimize as well as subqueries
- Indexes needed:
  - customers(created_at, email)
  - orders(customer_id, order_date, status)
- Consider materialized view if run frequently
- For very large datasets, pre-aggregate to monthly summary table

Execution time: ~500ms on 1M customers, 5M orders (with indexes)

Alternative for better performance:
```sql
-- Use window functions instead of multiple CTEs
WITH cohort_data AS (
    SELECT
        c.id,
        DATE_TRUNC('month', c.created_at) AS cohort_month,
        FIRST_VALUE(DATE_TRUNC('month', o.order_date)) OVER (
            PARTITION BY c.id ORDER BY o.order_date
        ) AS first_order_month
    FROM customers c
    LEFT JOIN orders o ON c.id = o.customer_id AND o.status = 'completed'
    WHERE c.created_at >= '2023-01-01' AND c.created_at < '2024-01-01'
)
SELECT ...
-- Rest of query
```
```

---

## Database Design

### 4. Database Schema Design

**Purpose:** Design database schema for an application.

**Prompt:**
```
Design a database schema for [APPLICATION]:

Requirements:
- Application type: [WEB_APP/MOBILE/ETC]
- Data to store: [ENTITIES_AND_RELATIONSHIPS]
- Scale expectations: [USERS/DATA_VOLUME]
- Query patterns: [READ/WRITE_RATIOS and COMMON_QUERIES]
- Constraints: [BUSINESS_RULES]

Provide:
- Entity-Relationship description
- Table definitions (columns, data types, constraints)
- Primary keys and foreign keys
- Indexes for performance
- Constraints (unique, check, not null)
- Database type recommendation: [SQL/NOSQL]
- Normalization level: [1NF/2NF/3NF/DENORMALIZED]
- Relationships: [ONE_TO_ONE/ONE_TO_MANY/MANY_TO_MANY]

Include CREATE TABLE statements and rationale for design decisions.
```

**Example:**
```
Design schema for E-commerce Platform:

Requirements:
- Web app with mobile API
- Data: Users, products, orders, categories, reviews, payments
- Scale: 100k users, 50k products, 1M orders/year
- Query patterns: 80% reads (product browsing), 20% writes (orders)
- Constraints: One user per email, products must have category, orders must have payment

Schema Design:

Entity-Relationship:
- Users → Orders (one-to-many)
- Orders → OrderItems → Products (many-to-many through OrderItems)
- Products → Categories (many-to-one)
- Products ← Reviews ← Users (many-to-many, reviews link both)
- Orders → Payments (one-to-one or one-to-many if payment plans)

Tables:

1. users
```sql
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,  -- Business rule: unique email
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    phone VARCHAR(20),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP WITH TIME ZONE  -- Soft deletes
);

-- Indexes
CREATE INDEX idx_users_email ON users(email) WHERE deleted_at IS NULL;  -- Partial index
CREATE INDEX idx_users_created_at ON users(created_at);

-- Rationale:
-- - BIGSERIAL for future scale
-- - Email unique at DB level
-- - password_hash not password (security)
-- - Soft deletes (deleted_at) preserve history
-- - Timestamps for audit trail
```

2. categories
```sql
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    slug VARCHAR(100) NOT NULL UNIQUE,  -- URL-friendly
    parent_id INTEGER REFERENCES categories(id),  -- Self-referencing for hierarchy
    description TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_categories_parent_id ON categories(parent_id);
CREATE INDEX idx_categories_slug ON categories(slug);

-- Rationale:
-- - Hierarchical categories (parent_id allows subcategories)
-- - Slug for SEO-friendly URLs
-- - Small table, SERIAL sufficient
```

3. products
```sql
CREATE TABLE products (
    id BIGSERIAL PRIMARY KEY,
    category_id INTEGER NOT NULL REFERENCES categories(id),  -- Required
    name VARCHAR(200) NOT NULL,
    slug VARCHAR(200) NOT NULL UNIQUE,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL CHECK (price >= 0),  -- Non-negative
    stock_quantity INTEGER NOT NULL DEFAULT 0 CHECK (stock_quantity >= 0),
    sku VARCHAR(50) UNIQUE,  -- Stock keeping unit
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Indexes (read-heavy, optimize queries)
CREATE INDEX idx_products_category_id ON products(category_id);
CREATE INDEX idx_products_slug ON products(slug);
CREATE INDEX idx_products_sku ON products(sku);
CREATE INDEX idx_products_active_created ON products(is_active, created_at DESC);  -- Composite

-- Rationale:
-- - DECIMAL for money (avoid float precision issues)
-- - CHECK constraints enforce business rules at DB level
-- - SKU unique for inventory management
-- - Composite index for "active products ordered by date" query
```

4. orders
```sql
CREATE TABLE orders (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id),
    order_number VARCHAR(50) NOT NULL UNIQUE,  -- Human-readable: ORD-2023-001234
    status VARCHAR(20) NOT NULL DEFAULT 'pending',
        CHECK (status IN ('pending', 'processing', 'shipped', 'delivered', 'cancelled')),
    subtotal DECIMAL(10, 2) NOT NULL,
    tax DECIMAL(10, 2) NOT NULL DEFAULT 0,
    shipping_cost DECIMAL(10, 2) NOT NULL DEFAULT 0,
    total_amount DECIMAL(10, 2) NOT NULL,
    shipping_address_id BIGINT REFERENCES addresses(id),  -- Assuming addresses table
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,

    -- Constraint: total should equal subtotal + tax + shipping
    CONSTRAINT check_order_total CHECK (total_amount = subtotal + tax + shipping_cost)
);

CREATE INDEX idx_orders_user_id ON orders(user_id);
CREATE INDEX idx_orders_order_number ON orders(order_number);
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_orders_created_at ON orders(created_at DESC);  -- Recent orders first

-- Rationale:
-- - order_number for human reference (emails, CS)
-- - ENUM-like CHECK constraint for status (better than separate table for few values)
-- - Store calculated fields (subtotal, tax, total) for historical accuracy
-- - CHECK constraint ensures data integrity
```

5. order_items (junction table)
```sql
CREATE TABLE order_items (
    id BIGSERIAL PRIMARY KEY,
    order_id BIGINT NOT NULL REFERENCES orders(id) ON DELETE CASCADE,
    product_id BIGINT NOT NULL REFERENCES products(id),
    quantity INTEGER NOT NULL CHECK (quantity > 0),
    unit_price DECIMAL(10, 2) NOT NULL,  -- Price at time of order (immutable)
    total_price DECIMAL(10, 2) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT check_item_total CHECK (total_price = quantity * unit_price),
    UNIQUE(order_id, product_id)  -- One line item per product per order
);

CREATE INDEX idx_order_items_order_id ON order_items(order_id);
CREATE INDEX idx_order_items_product_id ON order_items(product_id);

-- Rationale:
-- - Junction table for many-to-many (orders ↔ products)
-- - Store price at time of order (immutable, even if product price changes)
-- - CASCADE on delete (if order deleted, remove items)
-- - UNIQUE prevents duplicate products in same order
```

6. reviews
```sql
CREATE TABLE reviews (
    id BIGSERIAL PRIMARY KEY,
    product_id BIGINT NOT NULL REFERENCES products(id) ON DELETE CASCADE,
    user_id BIGINT NOT NULL REFERENCES users(id),
    rating INTEGER NOT NULL CHECK (rating BETWEEN 1 AND 5),
    title VARCHAR(200),
    comment TEXT,
    is_verified_purchase BOOLEAN DEFAULT FALSE,  -- Did they actually buy it?
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,

    UNIQUE(product_id, user_id)  -- One review per user per product
);

CREATE INDEX idx_reviews_product_id ON reviews(product_id);
CREATE INDEX idx_reviews_user_id ON reviews(user_id);
CREATE INDEX idx_reviews_rating ON reviews(rating);  -- Filter by rating

-- Rationale:
-- - Rating constrained to 1-5
-- - is_verified_purchase for trust/filtering
-- - UNIQUE prevents multiple reviews from same user
```

7. payments
```sql
CREATE TABLE payments (
    id BIGSERIAL PRIMARY KEY,
    order_id BIGINT NOT NULL REFERENCES orders(id),
    payment_method VARCHAR(50) NOT NULL,  -- 'credit_card', 'paypal', etc.
    amount DECIMAL(10, 2) NOT NULL,
    status VARCHAR(20) NOT NULL DEFAULT 'pending',
        CHECK (status IN ('pending', 'processing', 'completed', 'failed', 'refunded')),
    transaction_id VARCHAR(255),  -- External payment gateway ID
    processed_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,

    UNIQUE(transaction_id)  -- Prevent duplicate processing
);

CREATE INDEX idx_payments_order_id ON payments(order_id);
CREATE INDEX idx_payments_status ON payments(status);
CREATE INDEX idx_payments_transaction_id ON payments(transaction_id);

-- Rationale:
-- - One-to-many (order can have multiple payment attempts)
-- - Store transaction_id for reconciliation with payment gateway
-- - Status tracking for payment lifecycle
```

Additional Tables (mentioned but not detailed):
- addresses (shipping/billing addresses)
- product_images (one-to-many with products)
- cart_items (temporary, session-based)
- wishlists

Database Type: PostgreSQL
- Why: Relational data, ACID transactions critical for orders/payments
- Rich data types (JSONB for flexible attributes)
- Good performance at this scale
- Strong consistency needed for inventory/payments

Normalization: 3NF with pragmatic denormalization
- 3NF: No redundancy, referential integrity
- Denormalization: Store price in order_items (historical accuracy trumps normalization)

Design Decisions:
1. Soft deletes for users (preserve order history)
2. Immutable prices in order_items (historical record)
3. Check constraints for data integrity at DB level
4. Indexes optimized for read-heavy workload
5. DECIMAL for money (precision)
6. Timestamps with timezone (international app)
7. Unique constraints prevent duplicates
8. Foreign keys with appropriate CASCADE rules

Performance Optimization:
- Composite indexes for common query patterns
- Partial indexes (e.g., active products only)
- Consider partitioning orders by date if > 10M rows

Future Considerations:
- Sharding by user_id if scale exceeds single DB
- Read replicas for product browsing
- Cache layer (Redis) for product catalog
- Event sourcing for order state changes (audit trail)
```

---

## Data Analysis

### 5. Exploratory Data Analysis

**Purpose:** Generate code for exploring and understanding datasets.

**Prompt:**
```
Create exploratory data analysis (EDA) for [DATASET]:

Dataset details:
- Source: [FILE_FORMAT/DATABASE/API]
- Size: [ROWS/COLUMNS]
- Content: [WHAT_DATA_REPRESENTS]
- Goal: [WHAT_TO_DISCOVER]

EDA should include:
- Load and preview data
- Data types and structure
- Missing values analysis
- Summary statistics (mean, median, std, etc.)
- Distribution of key variables (histograms)
- Correlation analysis
- Outlier detection
- Key insights and patterns
- Data quality issues
- Visualizations (describe what to plot)
- Recommendations for cleaning/preprocessing

Language: [PYTHON/R]
Libraries: [PANDAS/NUMPY/MATPLOTLIB/SEABORN/ETC]
```

**Example:**
```
EDA for Customer Churn Dataset:

Dataset:
- Source: CSV file (customer_data.csv)
- Size: 10,000 rows, 20 columns
- Content: Customer demographics, usage, and churn status
- Goal: Understand factors related to customer churn

Python EDA Code:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

# Set style
sns.set_style('whitegrid')
plt.rcParams['figure.figsize'] = (12, 6)

# 1. Load and preview data
df = pd.read_csv('customer_data.csv')

print("Dataset Shape:", df.shape)
print("\nFirst 5 rows:")
print(df.head())

print("\nColumn Names:")
print(df.columns.tolist())

# 2. Data types and structure
print("\nData Types:")
print(df.dtypes)

print("\nDataset Info:")
df.info()

# 3. Missing values analysis
print("\nMissing Values:")
missing = df.isnull().sum()
missing_pct = 100 * df.isnull().sum() / len(df)
missing_df = pd.DataFrame({
    'Missing Count': missing,
    'Percentage': missing_pct
}).sort_values('Percentage', ascending=False)
print(missing_df[missing_df['Missing Count'] > 0])

# Visualize missing data
plt.figure(figsize=(10, 6))
sns.heatmap(df.isnull(), cbar=False, yticklabels=False, cmap='viridis')
plt.title('Missing Data Heatmap')
plt.tight_layout()
plt.savefig('missing_data.png')

# 4. Summary statistics
print("\nSummary Statistics (Numerical):")
print(df.describe())

print("\nSummary Statistics (Categorical):")
print(df.describe(include=['object']))

# 5. Target variable distribution (Churn)
print("\nChurn Distribution:")
print(df['churn'].value_counts())
print(df['churn'].value_counts(normalize=True))

plt.figure(figsize=(8, 6))
df['churn'].value_counts().plot(kind='bar')
plt.title('Churn Distribution')
plt.xlabel('Churn')
plt.ylabel('Count')
plt.xticks(rotation=0)
plt.tight_layout()
plt.savefig('churn_distribution.png')

# 6. Distribution of numerical features
numerical_cols = df.select_dtypes(include=[np.number]).columns.tolist()

for col in numerical_cols:
    fig, axes = plt.subplots(1, 2, figsize=(12, 4))

    # Histogram
    df[col].hist(bins=30, ax=axes[0])
    axes[0].set_title(f'{col} - Histogram')
    axes[0].set_xlabel(col)
    axes[0].set_ylabel('Frequency')

    # Box plot
    df.boxplot(column=col, ax=axes[1])
    axes[1].set_title(f'{col} - Box Plot')
    axes[1].set_ylabel(col)

    plt.tight_layout()
    plt.savefig(f'distribution_{col}.png')
    plt.close()

# 7. Correlation analysis
print("\nCorrelation Matrix:")
correlation = df[numerical_cols].corr()
print(correlation)

plt.figure(figsize=(10, 8))
sns.heatmap(correlation, annot=True, fmt='.2f', cmap='coolwarm', center=0)
plt.title('Correlation Heatmap')
plt.tight_layout()
plt.savefig('correlation_heatmap.png')

# 8. Churn rate by categorical features
categorical_cols = ['gender', 'payment_method', 'contract_type']

for col in categorical_cols:
    churn_rate = df.groupby(col)['churn'].agg(['sum', 'count'])
    churn_rate['rate'] = churn_rate['sum'] / churn_rate['count']
    print(f"\nChurn Rate by {col}:")
    print(churn_rate)

    # Visualization
    plt.figure(figsize=(8, 6))
    churn_rate['rate'].plot(kind='bar')
    plt.title(f'Churn Rate by {col}')
    plt.ylabel('Churn Rate')
    plt.xlabel(col)
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.savefig(f'churn_by_{col}.png')
    plt.close()

# 9. Outlier detection (Z-score method)
for col in numerical_cols:
    z_scores = np.abs(stats.zscore(df[col].dropna()))
    outliers = (z_scores > 3).sum()
    print(f"{col}: {outliers} outliers (Z-score > 3)")

# 10. Feature relationships with churn
# Numerical features
for col in numerical_cols:
    plt.figure(figsize=(10, 6))
    df.boxplot(column=col, by='churn')
    plt.title(f'{col} by Churn Status')
    plt.suptitle('')
    plt.tight_layout()
    plt.savefig(f'{col}_by_churn.png')
    plt.close()

# 11. Key insights
print("\n=== KEY INSIGHTS ===")

# Churn rate
churn_rate = df['churn'].mean()
print(f"1. Overall churn rate: {churn_rate:.2%}")

# Age and churn
age_churn = df.groupby('churn')['age'].mean()
print(f"2. Average age - Churned: {age_churn[1]:.1f}, Retained: {age_churn[0]:.1f}")

# Tenure and churn
tenure_churn = df.groupby('churn')['tenure_months'].mean()
print(f"3. Average tenure - Churned: {tenure_churn[1]:.1f} months, Retained: {tenure_churn[0]:.1f} months")

# Contract type impact
contract_churn = df.groupby('contract_type')['churn'].mean()
print(f"4. Churn by contract type:")
print(contract_churn)

# 12. Data quality issues
print("\n=== DATA QUALITY ISSUES ===")

# Missing values
if missing[missing > 0].any():
    print("1. Missing values found in:", missing[missing > 0].index.tolist())
    print("   Action: Impute or remove rows/columns")

# Outliers
print("2. Outliers detected (see Z-score analysis above)")
print("   Action: Investigate and decide to cap, transform, or remove")

# Duplicates
duplicates = df.duplicated().sum()
print(f"3. Duplicate rows: {duplicates}")
if duplicates > 0:
    print("   Action: Remove duplicates")

# Imbalanced target
churn_counts = df['churn'].value_counts()
imbalance_ratio = churn_counts.max() / churn_counts.min()
print(f"4. Class imbalance ratio: {imbalance_ratio:.2f}:1")
if imbalance_ratio > 3:
    print("   Action: Consider SMOTE, class weights, or stratified sampling")

# 13. Recommendations
print("\n=== PREPROCESSING RECOMMENDATIONS ===")
print("1. Handle missing values: Impute with median/mode or use predictive models")
print("2. Encode categorical variables: One-hot encoding or label encoding")
print("3. Scale numerical features: StandardScaler or MinMaxScaler")
print("4. Handle outliers: Cap at 99th percentile or use robust scaling")
print("5. Address class imbalance: Use SMOTE or adjust class weights in model")
print("6. Feature engineering: Create interaction features, age groups, tenure bins")
print("7. Remove high-correlation features: Drop one from pairs with r > 0.9")

# Save processed dataset info
df.describe().to_csv('summary_statistics.csv')
correlation.to_csv('correlation_matrix.csv')

print("\nEDA complete. Visualizations saved as PNG files.")
```

Expected Insights:
- Churned customers have shorter tenure
- Month-to-month contracts have higher churn
- Specific payment methods correlate with churn
- Age distribution differences between churned/retained
- Missing data patterns (e.g., missing income for younger customers)

Visualizations Created:
1. missing_data.png: Heatmap of missing values
2. churn_distribution.png: Bar chart of churn counts
3. distribution_*.png: Histograms and box plots for each numerical feature
4. correlation_heatmap.png: Feature correlations
5. churn_by_*.png: Churn rates by categorical features
6. *_by_churn.png: Feature distributions by churn status

Next Steps:
- Clean data based on findings
- Feature engineering
- Model building (logistic regression, random forest, XGBoost)
- Model evaluation and interpretation
```

---

### 6. Data Visualization

**Purpose:** Create visualizations to communicate data insights.

**Prompt:**
```
Create data visualizations for [DATA/ANALYSIS]:

Visualization goals:
- Data: [DATASET_DESCRIPTION]
- Message: [KEY_INSIGHT_TO_COMMUNICATE]
- Audience: [TECHNICAL/BUSINESS/EXECUTIVE]
- Format: [STATIC/INTERACTIVE/DASHBOARD]

Visualizations to create:
[LIST_OF_CHARTS and WHAT_EACH_SHOWS]

For each visualization specify:
- Chart type (bar, line, scatter, heatmap, etc.)
- Variables on axes
- Color/size encoding
- Annotations and labels
- Style preferences

Provide:
- Code to generate visualizations
- Explanation of design choices
- Tips for interpretation
- Tools: [MATPLOTLIB/PLOTLY/TABLEAU/D3/ETC]
```

**Example:**
```
Visualizations for Sales Performance Dashboard:

Data:
- Monthly sales by region, product category, salesperson
- 2 years of historical data
- Goal metrics: revenue, units sold, conversion rate

Message: Show sales trends, identify top performers, highlight underperforming regions

Audience: Sales leadership team

Format: Interactive dashboard (Plotly Dash)

Visualizations:

1. Revenue Trend Line Chart
- What: Monthly revenue over time with target line
- Chart: Multi-line chart
- X-axis: Month
- Y-axis: Revenue ($)
- Lines: Actual revenue (blue), Target (red dashed), Previous year (gray)
- Annotations: Label key events (product launches, promotions)

Code:
```python
import plotly.graph_objects as go
import pandas as pd

# Assuming df has columns: month, revenue, target, prev_year_revenue

fig = go.Figure()

# Actual revenue
fig.add_trace(go.Scatter(
    x=df['month'],
    y=df['revenue'],
    mode='lines+markers',
    name='Actual Revenue',
    line=dict(color='#0066FF', width=3),
    marker=dict(size=8)
))

# Target
fig.add_trace(go.Scatter(
    x=df['month'],
    y=df['target'],
    mode='lines',
    name='Target',
    line=dict(color='#FF0000', width=2, dash='dash')
))

# Previous year
fig.add_trace(go.Scatter(
    x=df['month'],
    y=df['prev_year_revenue'],
    mode='lines',
    name='Previous Year',
    line=dict(color='#999999', width=2),
    opacity=0.5
))

fig.update_layout(
    title='Monthly Revenue Trend',
    xaxis_title='Month',
    yaxis_title='Revenue ($)',
    hovermode='x unified',
    template='plotly_white',
    height=400
)

fig.show()
```

Design choices:
- Line chart: Shows trend over time clearly
- Multiple lines: Easy comparison of actual vs target vs last year
- Blue for actual: Standard for primary data
- Red dashed for target: Warning color, distinct line style
- Unified hover: Shows all values for a month simultaneously

2. Regional Performance Bar Chart
- What: Revenue by region with YoY growth %
- Chart: Grouped bar chart
- X-axis: Region
- Y-axis: Revenue
- Bars: This year (blue), Last year (gray)
- Annotations: Growth % above bars

```python
fig = go.Figure()

regions = df.groupby('region').agg({
    'revenue_2024': 'sum',
    'revenue_2023': 'sum'
}).reset_index()

regions['growth'] = 100 * (regions['revenue_2024'] - regions['revenue_2023']) / regions['revenue_2023']

fig.add_trace(go.Bar(
    x=regions['region'],
    y=regions['revenue_2024'],
    name='2024',
    marker_color='#0066FF',
    text=regions['growth'].apply(lambda x: f"+{x:.1f}%" if x > 0 else f"{x:.1f}%"),
    textposition='outside'
))

fig.add_trace(go.Bar(
    x=regions['region'],
    y=regions['revenue_2023'],
    name='2023',
    marker_color='#CCCCCC'
))

fig.update_layout(
    title='Revenue by Region (YoY Comparison)',
    xaxis_title='Region',
    yaxis_title='Revenue ($)',
    barmode='group',
    template='plotly_white',
    height=400
)

fig.show()
```

Design choices:
- Grouped bars: Clear comparison within each region
- Color contrast: Blue vs gray distinguishes years
- Growth % labels: Key metric visible at a glance
- Sorted by revenue: Most important regions first

3. Top Performers Leaderboard
- What: Top 10 salespeople by revenue
- Chart: Horizontal bar chart
- X-axis: Revenue
- Y-axis: Salesperson name
- Color: Gradient based on performance vs quota

```python
top_performers = df.groupby('salesperson').agg({
    'revenue': 'sum',
    'quota': 'first'
}).reset_index()

top_performers['quota_attainment'] = 100 * top_performers['revenue'] / top_performers['quota']
top_performers = top_performers.nlargest(10, 'revenue')

# Color scale: red < 80%, yellow 80-100%, green > 100%
colors = top_performers['quota_attainment'].apply(
    lambda x: '#10B981' if x >= 100 else '#F59E0B' if x >= 80 else '#EF4444'
)

fig = go.Figure(go.Bar(
    x=top_performers['revenue'],
    y=top_performers['salesperson'],
    orientation='h',
    marker=dict(color=colors),
    text=top_performers['quota_attainment'].apply(lambda x: f"{x:.0f}%"),
    textposition='inside'
))

fig.update_layout(
    title='Top 10 Salespeople by Revenue',
    xaxis_title='Revenue ($)',
    yaxis_title='',
    yaxis={'categoryorder':'total ascending'},  # Smallest at bottom
    template='plotly_white',
    height=500
)

fig.show()
```

Design choices:
- Horizontal bars: Easier to read names
- Color-coded: Instant visual of performance level (red/yellow/green)
- Quota attainment %: Shows performance vs goals
- Sorted ascending: Top performer at top

4. Product Category Treemap
- What: Revenue contribution by product category
- Chart: Treemap
- Size: Revenue
- Color: Profit margin %

```python
category_data = df.groupby('category').agg({
    'revenue': 'sum',
    'profit': 'sum'
}).reset_index()

category_data['margin'] = 100 * category_data['profit'] / category_data['revenue']

fig = go.Figure(go.Treemap(
    labels=category_data['category'],
    parents=[''] * len(category_data),  # All top-level
    values=category_data['revenue'],
    marker=dict(
        colorscale='RdYlGn',  # Red to yellow to green
        cmid=15,  # Center at 15% margin
        colorbar=dict(title="Margin %"),
        line=dict(width=2, color='white')
    ),
    text=category_data['margin'].apply(lambda x: f"{x:.1f}% margin"),
    textposition='middle center',
    hovertemplate='<b>%{label}</b><br>Revenue: $%{value:,.0f}<br>%{text}<extra></extra>'
))

fig.update_layout(
    title='Product Category Revenue & Margin',
    template='plotly_white',
    height=500
))

fig.show()
```

Design choices:
- Treemap: Shows proportional contribution at a glance
- Size by revenue: Biggest categories most prominent
- Color by margin: Identifies high-profit vs high-volume
- RdYlGn scale: Red (low margin) to green (high margin)

5. Conversion Funnel
- What: Sales funnel from leads to closed deals
- Chart: Funnel chart
- Stages: Leads → Qualified → Proposal → Negotiation → Closed
- Values: Count at each stage

```python
funnel_data = {
    'stage': ['Leads', 'Qualified', 'Proposal', 'Negotiation', 'Closed'],
    'count': [10000, 5000, 2000, 1000, 600]
}

df_funnel = pd.DataFrame(funnel_data)
df_funnel['conversion'] = 100 * df_funnel['count'] / df_funnel['count'].iloc[0]

fig = go.Figure(go.Funnel(
    y=df_funnel['stage'],
    x=df_funnel['count'],
    textinfo='value+percent initial',
    marker=dict(color=["#0066FF", "#3385FF", "#66A3FF", "#99C2FF", "#CCD9FF"]),
    connector=dict(line=dict(color="#99C2FF", width=2))
))

fig.update_layout(
    title='Sales Conversion Funnel',
    template='plotly_white',
    height=500
)

fig.show()
```

Design choices:
- Funnel chart: Standard for conversion analysis
- Gradual color: Visual flow through stages
- Percent initial: Shows conversion at each stage
- Clear labels: Stage names and counts

Dashboard Layout:
```
┌─────────────────────────────────────────────┐
│  Sales Dashboard - Q4 2024                  │
├───────────────────┬─────────────────────────┤
│  Revenue Trend    │  Regional Performance   │
│  (line chart)     │  (bar chart)            │
├───────────────────┼─────────────────────────┤
│  Top Performers   │  Category Breakdown     │
│  (h-bar chart)    │  (treemap)              │
├───────────────────────────────────────────  ┤
│  Conversion Funnel (center, full-width)     │
└─────────────────────────────────────────────┘
```

Interactive Features:
- Date range filter (affects all charts)
- Region dropdown (filters other charts)
- Click on chart element to drill down
- Export to PDF button

Interpretation Tips:
1. Revenue Trend: Look for seasonality, compare to target
2. Regional Bars: Identify underperforming regions (negative growth)
3. Leaderboard: Red salespeople need support/coaching
4. Treemap: Balance between high-revenue and high-margin categories
5. Funnel: Bottlenecks show where to focus sales enablement

Tools Used:
- Plotly for interactive charts
- Dash for web dashboard
- Pandas for data manipulation
- Can export static images for presentations (fig.write_image())

Accessibility:
- High contrast colors
- Colorblind-friendly palette
- Alt text for screen readers
- Keyboard navigation support
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for writing effective data prompts
- **Backend:** See [coding-prompts.md](./coding-prompts.md) for implementing data processing code
- **Architecture:** See [architecture-prompts.md](./architecture-prompts.md) for data architecture design
