## Ingestion Layer — Pub/Sub
Pub/Sub is used as the ingestion layer to handle high-throughput, low-latency event streaming
from multiple producers (web, mobile, backend services). Topics are partitioned by event_time
and user_id to ensure parallelism and ordering where required. Retention is configured for
7 days to support replay and backfilling. Dead-letter topics are used for malformed events.

## Stream Processing — Dataflow
Dataflow (Apache Beam) is used for unified batch and streaming processing.
It performs schema validation, deduplication using event_id, windowed aggregations,
late-event handling using watermarks, and exactly-once processing semantics.
Checkpoints are stored in GCS for fault tolerance and replay.

## Storage — GCS Lakehouse
Data is stored in GCS using a Lakehouse pattern:

Bronze: Raw immutable events stored in Avro/Parquet partitioned by ingestion_date.
Silver: Cleaned and deduplicated data with enforced schema and quality checks.
Gold: Business-aggregated tables optimized for analytics and ML features.

Partitioning is done by event_date and region to optimize query pruning and cost.


## Data Warehouse — BigQuery
BigQuery is used as the analytical warehouse for BI and ad-hoc querying.
Tables are partitioned by event_date and clustered by user_id and product_id
to reduce scan cost and improve query performance. BI Engine is enabled for
sub-second dashboard latency. Data is loaded incrementally from the Gold layer
using MERGE statements to support late-arriving updates.

## Orchestration — Cloud Composer
Cloud Composer (Airflow) orchestrates batch pipelines, backfills, and dependency
management across ingestion, transformation, and BigQuery loading jobs.
DAGs manage retry policies, SLA monitoring, and data quality validation steps.


## Serving — Looker / Vertex AI
Looker consumes curated BigQuery datasets for real-time business dashboards.
Vertex AI Feature Store is used to serve curated Gold layer features for
machine learning models such as recommendation and churn prediction.

## Monitoring — Cloud Monitoring / Logging
Cloud Monitoring and Logging track pipeline latency, throughput, error rates,
and SLA violations. Custom metrics are published from Dataflow and Composer.
Alerting policies are configured for lag, failed DAGs, and data freshness breaches.

