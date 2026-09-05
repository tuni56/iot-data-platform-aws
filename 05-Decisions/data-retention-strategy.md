# Data Retention Strategy

## Purpose

The platform must retain telemetry data for analytics, operational investigations, and historical reporting while controlling storage costs.

---

## Raw Data Retention

Raw telemetry data is stored in Amazon S3.

Retention period:

* 90 days

Benefits:

* Operational troubleshooting
* Data recovery
* Historical validation

---

## Curated Data Retention

Processed datasets are retained for long-term analytics.

Retention period:

* 2 years

Benefits:

* Trend analysis
* Business reporting
* Predictive maintenance initiatives

---

## Archive Strategy

Historical data is transitioned to lower-cost storage tiers.

Mechanism:

* Amazon S3 Lifecycle Policies

Benefits:

* Reduced storage costs
* Automated data management
* Long-term preservation

---

## Data Deletion

Data exceeding retention requirements is automatically removed.

Benefits:

* Cost control
* Reduced operational overhead
* Compliance with retention policies

---

## Infrastructure Management

Retention policies are managed through Terraform.

Benefits:

* Consistency
* Auditability
* Reproducibility