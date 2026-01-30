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

At its core, an e-commerce platform must support:-

Functional Requirement for the E-Commerce platform :-
1. User accounts & authentication – allowing customers to create profiles, log in securely, and manage preferences.
2. Product catalog management – structured product listings with categories, filters, tags, and attributes.
3. Shopping cart and checkout – persistent, real-time carts and smooth checkout flows across devices.
4. Payment processing – secure handling of transactions, refunds, and regional payment options.
5. Order management – end-to-end order lifecycle including tracking, shipping, and returns.
6. Search & recommendations – intelligent search capabilities and personalized product suggestions.
7. Analytics & reporting – dashboards for business insights like conversion rates, cart abandonment, and revenue trends.

Non-functional requirements:-
To keep customers engaged and businesses operational, the system must also guarantee:

1. Scalability – handling seasonal peaks like Black Friday or sudden viral traffic.
2. Availability – ensuring 24/7 uptime with minimal downtime.
3. Performance – low latency for search queries, checkout flows, and API responses.
4. Consistency & reliability – ensuring inventory updates and order statuses are always accurate.
5. Security & compliance – safeguarding customer data and adhering to standards like PCI DSS, GDPR, and CCPA.