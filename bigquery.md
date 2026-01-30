Data Structuer for the BigQuery

Bronze Layer:-
raw_clicks
raw_userid
raw_ingestionid

dataset:-
 - raw_click_events
  - raw_order_events
  - raw_payment_events

Silver Layer:-
exact_userid
exact_orderid

dataset:-
 - cleaned_click_events
  - deduped_orders
  - validated_payments

Gold Layer:-
final_userid
final_orderod

gold_dataset:-
- daily_sales_metrics
  - customer_lifetime_value
  - product_performance

# Partitioning Strategy(second thought):
1. order_date would be the partitioning key to fetch the latest order and keep track of latest order.
2. Easy to scan the table low cost as scan will be applying on fewer tables
3. handling the late arriving data with order date fullfiling the orders first and analysing based on the order date

# Partitioning Strategy
All fact tables are partitioned by event_date (DATE).
This enables partition pruning, reducing scanned data and cost.
Late events are handled using ingestion-time vs event-time partitions.

# Clustering Strategy
1. can be cluster on user_id, product_id, order_id
2. with the help of user_id, product_id and order-id easy to filter on unique records reduces cost and improves performance
3. For looker dahsboard it will easy to fetch the unique data, deduplication will eliminate and improves perfrmance, scaning will be on less data 

BigQuery Data Design
Dataset Structure
Bronze Dataset (bronze_ds)

Raw immutable event data stored for replay and audit.

Tables:
raw_click_events
raw_order_events
raw_payment_events

Characteristics:
Append-only
No deduplication
Schema enforced but no transformations
Stored for long-term retention and reprocessing

Silver Dataset (silver_ds)
Cleaned, validated, and deduplicated data.

Tables:
cleaned_click_events
deduped_orders
validated_payments

Transformations:
Schema validation
Deduplication using event_id
Filtering invalid or corrupt records
Standardized timestamps and IDs

Gold Dataset (gold_ds)
Business-level aggregated and curated tables.

Tables:
daily_sales_metrics
customer_lifetime_value
product_performance

Used by:
Looker dashboards
Ad-hoc analytics
ML feature generation

Partitioning Strategy (Critical)
All large fact tables are partitioned by event_date (DATE).

Why:
Enables partition pruning, reducing scanned data and query cost
Supports efficient time-range queries
Aligns with business reporting (daily metrics)

Late-arriving data:
Event-time partitioning is used
A configurable backfill window (e.g., last 3–7 days) is reprocessed daily
BigQuery MERGE statements update existing partitions safely

Clustering Strategy
Tables are clustered on:
user_id
product_id
order_id

Why:
These are high-cardinality columns frequently used in filters and joins
Clustering reduces data scanned within partitions
Improves join performance between fact and dimension tables
Significantly improves Looker dashboard query latency

Exactly-Once & Deduplication
Each event contains a unique event_id
Deduplication occurs in the Silver layer
BigQuery MERGE is used to ensure idempotent writes
Prevents duplicate orders and payment records during retries and replays

Cost Optimization
Partition pruning minimizes scanned bytes
Clustering improves query efficiency
Materialized views are used for frequently accessed KPIs
BI Engine is enabled for low-latency Looker dashboards
Historical data is queried only when required