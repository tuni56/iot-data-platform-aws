# Architecture

## Overview

The platform provides remote operational monitoring for industrial pumps deployed across rural and geographically distributed locations throughout Latin America.

The solution is designed using AWS serverless services and follows an event-driven architecture capable of supporting intermittent connectivity, operational observability, and scalable analytics.

The architecture is designed for a fleet of approximately 5,000 pumps while the demonstration environment simulates 500 pumps.

---

# Business Drivers

The architecture addresses the following challenges:

* Remote deployments with unreliable internet connectivity
* Limited visibility into equipment health
* Delayed incident detection
* Lack of centralized telemetry
* Need for cost-efficient analytics at scale

---

# Architecture Principles

### Serverless First

Operational overhead should be minimized through managed AWS services.

### Reliability First

Telemetry loss must be minimized through buffering, retry mechanisms, and dead-letter queues.

### Observability First

Every component must expose logs, metrics, and operational signals.

### Analytics Ready

Data must be stored in formats optimized for analytical workloads.

---

# Logical Architecture

```text
Pump Simulator
       │
       ▼
Local Buffer
       │
       ▼
AWS IoT Core
       │
       ▼
IoT Rule
       │
       ▼
SQS Ingestion Queue
       │
       ▼
Lambda Validation
       │
       ├──────────────► CloudWatch Metrics
       │
       ├──────────────► CloudWatch Logs
       │
       ▼
S3 Raw
       │
       ▼
Glue ETL
       │
       ▼
S3 Curated (Parquet)
       │
       ▼
Glue Catalog
       │
       ▼
Athena


Lambda Failures
       │
       ▼
SQS DLQ
       │
       ▼
CloudWatch Alarm
       │
       ▼
SNS Notification
```

---

# Component Responsibilities

## Pump Simulator

Generates telemetry events that emulate industrial pump behavior.

The simulator supports:

* RS 5x5 pumps
* AC 44 pumps
* AC 66 pumps

Telemetry is generated every minute.

---

## Local Buffer

Provides temporary local storage during connectivity interruptions.

Implements:

* Store-and-forward pattern
* Retry logic
* Delayed delivery support

---

## AWS IoT Core

Secure device ingestion layer.

Responsibilities:

* Device authentication
* MQTT communication
* Message routing

AWS IoT Rules can route MQTT messages directly to Amazon SQS.

---

## SQS Ingestion Queue

Decouples telemetry ingestion from downstream processing.

Benefits:

* Improved resilience
* Retry support
* Traffic smoothing

---

## Lambda Validation

Performs lightweight processing.

Responsibilities:

* Schema validation
* Data quality checks
* Basic anomaly detection
* Custom metrics publication

Lambda does not perform analytical transformations.

---

## S3 Raw

Stores telemetry exactly as received.

Format:

JSON

Purpose:

* Auditability
* Replay capability
* Raw data preservation

---

## Glue ETL

Transforms raw telemetry into analytical datasets.

Responsibilities:

* Data cleansing
* Partition management
* JSON to Parquet conversion

---

## S3 Curated

Stores optimized analytical datasets.

Format:

Apache Parquet

Partitioning:

* year
* month
* day
* pump_model

---

## Glue Catalog

Provides centralized metadata management.

Used by:

* Athena
* Future analytical workloads

---

## Athena

Provides serverless analytics over curated telemetry datasets.

Supports:

* Operational reporting
* Historical analysis
* Trend identification

---

# Observability

## CloudWatch Logs

Enabled for:

* Lambda
* IoT processing
* ETL jobs

## CloudWatch Metrics

Operational metrics include:

* TelemetryReceived
* TelemetryProcessed
* TelemetryRejected
* RunningPumps
* FaultPumps
* LambdaErrors
* DLQMessages

## CloudWatch Alarms

Generated when:

* DLQ receives messages
* Lambda failures exceed threshold

## SNS Notifications

Operational alerts delivered through email subscriptions.

---

# Failure Handling

Validation failures are redirected to an SQS Dead Letter Queue.

Objectives:

* Prevent silent failures
* Preserve problematic messages
* Enable root cause analysis

AWS IoT Rules also support error actions when rule actions fail, providing additional resiliency options.

---

# Scalability

Target production scale:

* 5,000 pumps
* 7.2 million events/day

Demo scale:

* 500 pumps
* 720,000 events/day

The architecture can scale horizontally without redesign through managed AWS services.

