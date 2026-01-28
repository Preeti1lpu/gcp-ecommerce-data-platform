1️⃣ Functional Requirements

Event Types

User clickstream events (page_view, search, add_to_cart)

Order lifecycle events (order_created, order_confirmed, shipped, delivered, cancelled)

Payment events (payment_initiated, success, failure, refund)

Inventory events (stock_update, price_change)

Customer events (login, profile_update)

Data Sources

Web & mobile applications (real-time events via Pub/Sub)

Backend microservices (order, payment, inventory systems)

Third-party payment gateways

CRM system (batch ingestion)

Non-Functional Requirements
Scale
Daily Volume: ~50 million events/day

Peak Throughput: 80K–100K events/second during sale hours

Latency
Streaming analytics: ≤ 5 seconds end-to-end

Batch processing: ≤ 1 hour SLA

Data Retention
Raw data (Bronze): 5 years in GCS

Curated data (Silver/Gold): 3–5 years in BigQuery

Reliability & Availability

Exactly-once processing for orders and payments
99.9% pipeline availability

Automatic replay and backfill support

Security & Compliance

IAM-based access control (least privilege)

Encryption at rest (KMS) and in transit (TLS)

PII masking and tokenization in BigQuery

GDPR compliance (right to erasure, audit logs)

SLA & Observability

Data freshness SLA: <10 minutes for critical tables

Monitoring: pipeline lag, error rate, schema drift

Alerting on SLA breach, DAG failures, Pub/Sub backlog