# Technology Selection

## AWS IoT Core

Selected for secure MQTT ingestion and device authentication.

Reasons:

* Native IoT support
* X.509 certificates
* Managed service
* Automatic scaling

---

## Amazon SQS

Selected as ingestion buffer.

Reasons:

* Decouples producers and consumers
* Handles traffic spikes
* Supports DLQ integration

---

## AWS Lambda

Selected for telemetry validation and processing.

Reasons:

* Event-driven execution
* Serverless scaling
* Consumption-based pricing

---

## Amazon S3

Selected as the central data lake.

Reasons:

* Durability
* Scalability
* Cost efficiency
* Native AWS integration

---

## AWS Glue

Selected for data cataloging and ETL workloads.

Reasons:

* Managed Spark environment
* Native Athena integration
* Serverless operation

---

## Amazon Athena

Selected for analytics.

Reasons:

* No infrastructure management
* SQL interface
* Pay-per-query model

---

## Amazon CloudWatch

Selected for monitoring and observability.

Reasons:

* Native AWS integration
* Metrics
* Logs
* Alarms
* Dashboards

---

## Amazon SNS

Selected for notifications.

Reasons:

* Simple alert delivery
* Low operational cost
* Native CloudWatch integration

---

## Terraform

Selected for Infrastructure as Code.

Reasons:

* Industry standard
* AWS support
* Reproducibility
* Version control

---

## Technologies Not Selected

### Amazon MSK

Not required for projected data volume.

### Amazon Kinesis

Adds complexity without meaningful business value.

### Amazon EMR

Excessive for workload requirements.

### Amazon Redshift

Athena provides sufficient analytical capabilities for the expected data volume.

### Amazon EC2

Avoided to eliminate infrastructure management responsibilities.
