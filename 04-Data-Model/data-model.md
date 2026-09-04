Data Model
Overview

The platform collects telemetry from distributed industrial pumps operating in agricultural, industrial, and remote environments.

Each telemetry event represents a snapshot of the operational state of a pump at a specific point in time.

Event Structure

Telemetry is transmitted as JSON.

Example:

{
  "event_timestamp": "2026-10-15T14:35:00Z",
  "pump_id": "PUMP-004521",
  "site_id": "SITE-00218",
  "pump_model": "RS-5",
  "status": "RUNNING",
  "flow_rate_m3h": 82.4,
  "pressure_bar": 7.2,
  "motor_temperature_c": 68.5,
  "vibration_mm_s": 2.8,
  "power_kw": 24.1
}
Field Definitions
event_timestamp

UTC timestamp of the telemetry event.

Type:

TIMESTAMP

pump_id

Unique identifier of the pump.

Type:

STRING

Example:

PUMP-004521

site_id

Customer installation identifier.

Type:

STRING

Example:

SITE-00218

pump_model

Pump family.

Allowed values:

RS-5
AC-4
AC-6

Type:

STRING

status

Current operating state.

Allowed values:

RUNNING
STOPPED
MAINTENANCE
FAULT

Type:

STRING

flow_rate_m3h

Water flow rate.

Unit:

m³/hour

Type:

DOUBLE

pressure_bar

Discharge pressure.

Unit:

bar

Type:

DOUBLE

motor_temperature_c

Motor temperature.

Unit:

°C

Type:

DOUBLE

vibration_mm_s

Mechanical vibration.

Unit:

mm/s

Type:

DOUBLE

power_kw

Electrical consumption.

Unit:

kW

Type:

DOUBLE

Expected Data Quality Rules

event_timestamp must not be null

pump_id must not be null

site_id must not be null

pump_model must be valid

flow_rate_m3h >= 0

pressure_bar >= 0

motor_temperature_c >= 0

vibration_mm_s >= 0

power_kw >= 0

S3 Raw Storage Format

JSON

Purpose:

Preserve original telemetry exactly as received.

Curated Storage Format

Apache Parquet

Purpose:

Optimized analytical querying.

Benefits:

Reduced storage footprint
Faster Athena queries
Lower Athena query costs
Partition Strategy

Partition by:

year
month
day

Example:

s3://curated-bucket/year=2026/month=10/day=15/

Schema Evolution Strategy

New attributes may be added without rewriting historical data.

Examples:

battery_voltage
operating_hours
fuel_level
ambient_temperature

Backward compatibility must be preserved.
