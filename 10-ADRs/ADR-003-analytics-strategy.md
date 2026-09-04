ADR-003 – Analytics Processing Strategy
Status

Accepted

Context

The platform must provide operational visibility while remaining cost-efficient and simple to operate.

Several processing options were evaluated:

Real-time streaming analytics
Near real-time analytics
Batch analytics
Decision

Telemetry ingestion will occur continuously through AWS IoT Core.

Analytical processing will be performed using batch-oriented services and analytical queries through Amazon Athena.

Rationale

The business objective is operational visibility and historical analysis rather than sub-second decision making.

Batch analytics:

Reduces operational complexity
Minimizes infrastructure costs
Supports serverless architecture
Simplifies implementation
Consequences

Benefits:

Lower cost
Simpler architecture
Reduced operational burden

Trade-offs:

No real-time dashboards
No real-time alerting in phase 1

Future versions may incorporate streaming services if operational requirements evolve.
