# ADR-006 – Intermittent Connectivity Strategy

## Status

Accepted

---

## Context

The company operates thousands of pumps deployed across agricultural, industrial, and remote environments throughout Latin America.

Many installations are located in areas where internet connectivity is unreliable due to:

* Rural network limitations
* Cellular coverage gaps
* Power outages
* Severe weather conditions
* Natural disasters such as earthquakes and their aftershocks
* Infrastructure maintenance activities

Loss of connectivity must not result in loss of operational telemetry.

The platform must continue collecting information even when communication with AWS is temporarily unavailable.

---

## Decision

Telemetry-producing devices will implement a local buffering mechanism capable of storing telemetry events while disconnected from the cloud.

When connectivity is restored, buffered events will be transmitted automatically to AWS IoT Core in chronological order.

Additionally:

* Devices will implement automatic reconnection logic.
* Exponential backoff with jitter will be used during reconnection attempts.
* Telemetry events will retain their original timestamps.
* Cloud-side processing must support delayed event arrival.

This approach aligns with AWS IoT Well-Architected reliability recommendations for intermittent connectivity scenarios.

---

## Rationale

The primary objective is to prevent data loss during temporary communication failures.

A significant portion of the installed fleet operates in rural locations where continuous connectivity cannot be guaranteed.

Store-and-forward behavior enables:

* Reliable telemetry collection
* Historical data preservation
* Improved operational visibility
* More accurate analytical reporting

without requiring continuous network availability. AWS recommends local storage and later transmission of buffered messages when connectivity returns.

---

## Consequences

### Benefits

* No telemetry loss during temporary outages
* Improved resilience
* Better support for rural deployments
* Greater operational reliability
* Alignment with industrial IoT best practices

### Trade-offs

* Additional device-side logic
* Local storage requirements
* Potential ingestion bursts after reconnection
* Need to process late-arriving events

---

## Implementation Notes

Device software will maintain a persistent local queue.

During a connectivity interruption:

```text
Telemetry Generated
        ↓
Local Buffer
        ↓
Connection Unavailable
```

When connectivity is restored:

```text
Local Buffer
        ↓
AWS IoT Core
        ↓
Cloud Processing
```

Events will be transmitted using a store-and-forward pattern.

Future versions may evaluate AWS IoT Greengrass capabilities for advanced edge processing and buffering scenarios. AWS IoT guidance recommends durable local storage, automatic reconnection, and synchronization after connectivity restoration for remote and intermittently connected devices.
