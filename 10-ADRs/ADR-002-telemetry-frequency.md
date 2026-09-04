ADR-002 – Telemetry Frequency
Status

Accepted

Context

The platform is intended to monitor distributed industrial pumps operating in remote environments.

Telemetry frequency directly impacts:

Data volume
Storage costs
Query performance
Infrastructure requirements
Decision

Each pump will publish telemetry every minute.

Rationale

One-minute intervals provide sufficient operational visibility for:

Asset monitoring
Trend analysis
Anomaly detection
Performance reporting

while maintaining reasonable storage and processing costs.

The selected interval aligns with the monitoring requirements of irrigation systems, water transfer operations, and mobile pumping units.

Consequences

Expected production scale:

5,000 pumps
7.2 million events/day

Demo scale:

500 pumps
720,000 events/day

The architecture remains capable of supporting higher frequencies if required in future phases.
