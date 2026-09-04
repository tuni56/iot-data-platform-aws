# ADR-007 – Backup and Disaster Recovery Strategy

## Status

Accepted

---

## Context

The platform supports operational monitoring for industrial pumps deployed across geographically distributed locations.

Telemetry data represents operational history and business-critical information that must remain available even during infrastructure failures.

The disaster recovery strategy must balance:

* Reliability
* Cost
* Operational complexity
* Business requirements

---

## Decision

The platform will adopt a disaster recovery strategy aligned with AWS Well-Architected Framework recommendations.

The initial implementation will use:

```text
Single Region
Multi-AZ
```

combined with:

* Infrastructure as Code (Terraform)
* Amazon S3 Versioning
* Source code stored in GitHub
* Managed AWS services with built-in Multi-AZ resilience
* Documented recovery procedures

---

## Recovery Objectives

### Recovery Time Objective (RTO)

```text
4 Hours
```

Maximum acceptable service restoration time following a regional disruption.

---

### Recovery Point Objective (RPO)

```text
15 Minutes
```

Maximum acceptable data loss window.

---

## Backup Strategy

### Amazon S3

Versioning enabled for:

* Raw telemetry bucket
* Curated telemetry bucket
* Terraform state bucket

Purpose:

* Protection against accidental deletion
* Recovery of previous object versions
* Operational resilience

---

### Infrastructure

All infrastructure is defined through Terraform.

Recovery process:

```text
Terraform State
        +
Terraform Code
        =
Environment Recreation
```

---

### Source Code

Application code and documentation are maintained in GitHub repositories.

This provides:

* Version history
* Recovery capability
* Change tracking

---

## Disaster Recovery Approach

The initial architecture relies on AWS managed services operating across multiple Availability Zones within a single AWS Region.

This approach provides:

* High availability
* Simplified operations
* Reduced costs
* Faster implementation

while remaining aligned with expected business requirements.

---

## Future Evolution

The architecture is designed to evolve toward:

```text
Cross-Region Recovery
```

through:

* S3 Cross-Region Replication
* Secondary telemetry storage
* Secondary analytics environment
* Regional failover procedures

These capabilities will be evaluated when business growth or contractual SLAs justify the additional operational complexity and cost.

---

## Rationale

AWS recommends selecting disaster recovery patterns according to business objectives rather than adopting multi-region architectures by default.

For this workload, a Single Region Multi-AZ design provides the most appropriate balance between:

* Reliability
* Simplicity
* Cost efficiency
* Operational maturity

---

## Consequences

### Benefits

* Reduced operational complexity
* Lower infrastructure costs
* Faster deployment
* Strong baseline resilience

### Trade-offs

* Regional failures require recovery procedures
* Cross-region failover is not automatic in the initial version

The architecture remains prepared for future multi-region expansion without requiring major redesign.
