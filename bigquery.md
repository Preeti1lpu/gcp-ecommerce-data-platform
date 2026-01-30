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