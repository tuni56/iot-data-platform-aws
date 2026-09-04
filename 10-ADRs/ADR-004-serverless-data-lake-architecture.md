# ADR-004 – Serverless Data Lake Architecture

## Status

Accepted

---

## Context

The platform must ingest telemetry from thousands of distributed industrial pumps while minimizing operational complexity and infrastructure management.

The solution should:

* Scale automatically
* Support analytical workloads
* Minimize operational overhead
* Remain cost-efficient
* Support future expansion

---

## Decision

The platform will adopt a fully serverless architecture based on:

AWS IoT Core

↓

Amazon SQS

↓

AWS Lambda

↓

Amazon S3 Raw

↓

AWS Glue

↓

Amazon S3 Curated (Parquet)

↓

AWS Glue Catalog

↓

Amazon Athena

---

## Rationale

Managed AWS services eliminate infrastructure administration while providing built-in scalability and high availability.

The architecture separates:

* Ingestion
* Validation
* Storage
* Transformation
* Analytics

allowing each layer to evolve independently.

---

## Consequences

Benefits:

* No servers to manage
* Automatic scaling
* Pay-per-use pricing
* Simplified operations
* Faster delivery

Trade-offs:

* Service limits must be monitored
* Greater dependency on AWS managed services
* Vendor-specific implementation
