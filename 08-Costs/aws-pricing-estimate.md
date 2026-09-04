# AWS Pricing Estimate

## Purpose

This document provides a high-level cost estimate for the Industrial IoT Monitoring Platform.

The objective is not to calculate exact AWS charges but to evaluate architectural decisions and identify the primary cost drivers.

All values should be considered indicative and may vary depending on AWS Region, telemetry volume, retention policies, and operational usage.

---

# Environment Scenarios

## Demo Environment

Fleet Size:

* 500 pumps

Daily Events:

* 23,060 telemetry events

Monthly Events:

* ~691,800 telemetry events

---

## Production Environment

Fleet Size:

* 5,000 pumps

Daily Events:

* 230,600 telemetry events

Monthly Events:

* ~6.9 million telemetry events

---

# Service Cost Drivers

## AWS IoT Core

Primary cost driver:

* MQTT message ingestion

Production Estimate:

Approximately 7 million messages/month.

Expected Cost Impact:

Low

Rationale:

Telemetry frequency was intentionally optimized according to equipment criticality.

---

## Amazon SQS

Primary cost driver:

* Queue requests

Production Estimate:

Approximately 7 million messages/month.

Expected Cost Impact:

Very Low

Rationale:

Amazon SQS is one of the lowest-cost managed services in the architecture.

---

## AWS Lambda

Primary cost drivers:

* Invocations
* Execution duration

Production Estimate:

Approximately 7 million invocations/month.

Expected Cost Impact:

Low

Rationale:

Validation logic remains lightweight and stateless.

No heavy transformations are executed inside Lambda.

---

## Amazon S3

Primary cost drivers:

* Storage volume
* API requests

Estimated Annual Storage:

Approximately 21 GB/year.

Expected Cost Impact:

Very Low

Rationale:

Telemetry payloads are small and highly structured.

---

## AWS Glue

Primary cost drivers:

* ETL execution time
* Data processing volume

Expected Cost Impact:

Medium

Rationale:

Glue performs all analytical transformations and Parquet conversion.

This is likely to become one of the largest operational costs.

---

## Amazon Athena

Primary cost drivers:

* Data scanned per query

Expected Cost Impact:

Low

Mitigation Strategies:

* Parquet storage
* Partitioning
* Query optimization

Expected Reduction:

80–95% reduction in scanned data compared to raw JSON.

---

## CloudWatch

Primary cost drivers:

* Custom metrics
* Logs retention
* Dashboards

Expected Cost Impact:

Low to Medium

Rationale:

Observability is a core business requirement of the platform.

---

## SNS

Primary cost drivers:

* Notifications

Expected Cost Impact:

Negligible

---

# Relative Cost Distribution

Estimated cost contribution:

| Service    | Relative Impact |
| ---------- | --------------- |
| Glue       | High            |
| CloudWatch | Medium          |
| Athena     | Medium          |
| IoT Core   | Low             |
| Lambda     | Low             |
| S3         | Low             |
| SQS        | Very Low        |
| SNS        | Negligible      |

---

# FinOps Decisions

The following architectural decisions were made specifically to reduce long-term operational costs.

## Adaptive Telemetry

Different pump categories generate telemetry at different frequencies.

Benefit:

Reduces unnecessary message volume.

---

## Serverless Services

No EC2 instances are maintained.

Benefit:

Eliminates idle infrastructure costs.

---

## Parquet Storage

Analytical datasets are stored using Apache Parquet.

Benefit:

Lower Athena costs and faster queries.

---

## Data Partitioning

Partitions:

* year
* month
* day
* pump_model

Benefit:

Reduced query scan volume.

---

## Event-Driven Architecture

Processing occurs only when telemetry is received.

Benefit:

Pay only for actual usage.

---

# Cost Optimization Opportunities

Future improvements may include:

* Intelligent telemetry sampling
* Lifecycle policies for historical data
* Archival to Amazon S3 Glacier
* Automated cost anomaly detection
* FinOps dashboards

---

# Conclusion

The platform was designed to optimize operational visibility rather than support massive-scale data processing.

The architecture demonstrates that industrial IoT workloads can achieve high reliability, observability, and analytical capability while maintaining predictable and cost-efficient cloud spending.
