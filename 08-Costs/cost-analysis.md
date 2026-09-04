# Cost Analysis

## Executive Summary

The architecture was designed to optimize operational visibility rather than process massive data volumes.

Although the platform supports thousands of distributed industrial pumps, telemetry generation remains relatively modest due to business-driven sampling frequencies.

As a result, the solution achieves:

* Low infrastructure costs
* Minimal operational overhead
* Predictable scaling
* Cost-efficient analytics

while maintaining production-grade reliability and observability.

---

# Fleet Assumptions

## Production Environment

| Pump Type                   | Quantity |
| --------------------------- | -------: |
| RS 5x5 Irrigation Pumps     |    3,000 |
| AC 44 Transfer Pumps        |    1,800 |
| AC 66 Fire Protection Pumps |      200 |
| Total Fleet                 |    5,000 |

---

## Demonstration Environment

| Pump Type                   | Quantity |
| --------------------------- | -------: |
| RS 5x5 Irrigation Pumps     |      300 |
| AC 44 Transfer Pumps        |      180 |
| AC 66 Fire Protection Pumps |       20 |
| Total Fleet                 |      500 |

---

# Telemetry Generation

## RS 5x5

Frequency:

48 events/day

Daily Events:

300 × 48 = 14,400

---

## AC 44

Frequency:

48 events/day

Daily Events:

180 × 48 = 8,640

---

## AC 66

Standby Frequency:

1 event/day

Daily Events:

20 × 1 = 20

---

## Total Daily Events (Demo)

14,400 + 8,640 + 20

= 23,060 events/day

---

## Total Daily Events (Production)

144,000 + 86,400 + 200

= 230,600 events/day

---

# Storage Estimation

Average Telemetry Record:

250 bytes

Daily Storage:

230,600 × 250 bytes

≈ 57.6 MB/day

Annual Storage:

≈ 21 GB/year

---

# Cost Optimization Decisions

## Adaptive Telemetry Frequency

Not all pumps generate telemetry at the same rate.

Data collection frequency is aligned with operational criticality.

Benefits:

* Reduced storage costs
* Lower ingestion costs
* Better signal-to-noise ratio

---

## Serverless Architecture

The platform uses:

* AWS IoT Core
* Amazon SQS
* AWS Lambda
* Amazon S3
* AWS Glue
* Amazon Athena

No EC2 instances are required.

Benefits:

* No server administration
* Automatic scaling
* Consumption-based pricing

---

## Parquet Storage

Curated datasets are stored using Apache Parquet.

Expected benefits:

* 80–95% reduction in scanned data
* Faster analytical queries
* Lower Athena costs

---

## Data Partitioning

Partitions:

* year
* month
* day
* pump_model

Benefits:

* Reduced query latency
* Reduced Athena scanning costs

---

# Operational Cost Drivers

The primary cost drivers are:

1. AWS IoT Core message ingestion
2. AWS Glue processing
3. Athena query execution
4. CloudWatch metrics and logs

Storage costs remain relatively small due to the low annual data volume.

---

# FinOps Considerations

The platform was intentionally designed to minimize idle infrastructure.

Key principles:

* Pay only for usage
* Eliminate permanently running servers
* Store data using efficient columnar formats
* Capture telemetry according to business requirements

This approach aligns technical architecture with operational and financial efficiency.

---

# Conclusion

The platform demonstrates that industrial IoT solutions do not necessarily require large-scale data infrastructure.

For this workload, the primary challenge is not data volume but operational visibility across geographically distributed assets operating in environments with intermittent connectivity.

The architecture therefore prioritizes:

* Reliability
* Observability
* Cost efficiency
* Operational simplicity

while remaining capable of scaling as business requirements evolve.
