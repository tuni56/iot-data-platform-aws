# Observability Strategy

## Purpose

The primary objective of the platform is to provide operational visibility across geographically distributed industrial pumps operating in environments with intermittent connectivity.

Observability is therefore considered a core business capability rather than a technical afterthought.

The platform follows an "Observability First" principle, ensuring that all critical components emit operational signals, metrics, logs, and alerts.

---

# Observability Objectives

The platform must provide visibility into:

* Fleet health
* Telemetry ingestion
* Data quality
* Processing failures
* Connectivity issues
* Operational incidents

---

# Observability Pillars

## Metrics

Metrics provide real-time visibility into platform health and business operations.

### Fleet Metrics

* RunningPumps
* StoppedPumps
* FaultPumps
* ActiveFirePumps

### Telemetry Metrics

* TelemetryReceived
* TelemetryProcessed
* TelemetryRejected
* LateArrivingEvents

### Data Quality Metrics

* InvalidSchemaEvents
* MissingRequiredFields
* InvalidMeasurements

### Reliability Metrics

* LambdaErrors
* LambdaTimeouts
* DLQMessages
* FailedValidations

---

## Logs

Structured JSON logging will be used across all processing components.

Each log event should include:

* timestamp
* pump_id
* pump_model
* event_type
* processing_status
* correlation_id

Purpose:

* Root cause analysis
* Incident investigation
* Auditability

---

## Dashboards

CloudWatch Dashboards will provide operational visibility.

### Fleet Dashboard

Displays:

* Active pumps
* Faulted pumps
* Fire pump status
* Telemetry volume

### Data Quality Dashboard

Displays:

* Invalid records
* Validation failures
* Late-arriving telemetry

### Reliability Dashboard

Displays:

* Lambda failures
* DLQ activity
* Alarm history

---

# Alerting Strategy

CloudWatch Alarms will trigger operational alerts.

## Critical Alerts

Examples:

* DLQ contains messages
* Lambda error rate exceeds threshold
* Fire pump reports critical fault
* Telemetry ingestion stops unexpectedly

Notification Channel:

Amazon SNS

---

## Warning Alerts

Examples:

* Increased validation failures
* Delayed telemetry arrival
* Elevated vibration measurements

Notification Channel:

Amazon SNS

---

# Operational KPIs

The platform will track:

* Telemetry Processing Success Rate
* Data Quality Score
* Fleet Availability
* Incident Detection Time
* Mean Time to Investigation (MTTI)

---

# Observability Architecture

```text
AWS IoT Core
        │
        ▼
SQS
        │
        ▼
Lambda Validation
        │
        ├── CloudWatch Logs
        ├── CloudWatch Metrics
        └── CloudWatch Alarms
                    │
                    ▼
                  SNS

SQS DLQ
        │
        ▼
CloudWatch Alarm
        │
        ▼
SNS
```

---

# Success Criteria

Operators must be able to answer the following questions within minutes:

* Is the platform healthy?
* Are pumps reporting telemetry?
* Are there active incidents?
* Are any pumps operating outside expected parameters?
* Are messages accumulating in the DLQ?
* Is telemetry quality degrading?

If these questions can be answered quickly, observability objectives are considered satisfied.
