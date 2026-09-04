# ADR-002 – Telemetry Frequency Strategy

## Status

Accepted

---

## Context

The company manufactures and supports centrifugal pumps used across agricultural, industrial, water transfer, and fire protection applications throughout Latin America.

Different pump categories operate under different business and operational requirements.

A single telemetry frequency would either:

* Generate unnecessary operational costs
* Fail to capture critical events when equipment is operating under emergency conditions

Telemetry collection must therefore be aligned with equipment criticality and operational behavior.

---

## Decision

Telemetry frequency will vary according to pump type and operating scenario.

---

## RS 5x5 Irrigation Pumps

Typical use:

* Agricultural irrigation
* Water distribution in rural environments

Telemetry frequency:

```text
Every 30 minutes
```

Collected variables:

* Flow rate (m³/h)
* Pressure
* Motor temperature
* Vibration
* Operational status

### Rationale

Irrigation systems typically operate under stable conditions for extended periods.

Capturing telemetry every 30 minutes provides sufficient operational visibility while minimizing infrastructure and storage costs.

---

## AC 44 Transfer and Water Supply Pumps

Typical use:

* Water transfer
* Reservoir filling
* Livestock watering systems
* Rural water distribution

Telemetry frequency:

```text
Every 30 minutes
```

Collected variables:

* Flow rate
* Total dynamic head
* Temperature
* Vibration
* Operational status

### Rationale

These pumps generally operate continuously with predictable workloads.

Thirty-minute telemetry intervals provide adequate monitoring while maintaining cost efficiency.

---

## AC 66 Fire Protection Pumps

Typical use:

* Fire protection systems
* Emergency pumping equipment
* Mobile firefighting units

### Standby Mode

Telemetry frequency:

```text
Once every 24 hours
```

Purpose:

* Verify equipment availability
* Confirm operational readiness

### Active Emergency Mode

Telemetry frequency:

```text
Every minute
```

Collected variables:

* RPM
* Flow rate
* Pressure
* Temperature
* Vibration

### Rationale

During a fire event, equipment performance becomes mission critical.

The prestaciones del equipo must remain within design specifications throughout the emergency operation.

High-frequency telemetry allows operators to identify performance degradation, overheating, excessive vibration, or pressure loss while the equipment is actively protecting people, infrastructure, and assets.

---

## Consequences

### Benefits

* Telemetry aligned with business needs
* Lower operational costs
* Reduced storage consumption
* Improved focus on critical assets
* Better operational efficiency

### Trade-offs

* Different monitoring policies per asset type
* More complex telemetry management logic

---

## Future Considerations

Future versions may support dynamic telemetry frequencies based on:

* Operating conditions
* Environmental factors
* Equipment health indicators
* Predictive maintenance models

This approach would allow the platform to increase telemetry frequency automatically when abnormal behavior is detected.

