# Requirements & Stakeholders

## Stakeholders

### Operations Manager

Responsible for monitoring pump fleet performance across all customer locations.

Needs:

* Visibility into equipment status
* Operational performance metrics
* Historical trend analysis

---

### Maintenance Team

Responsible for investigating abnormal equipment behavior.

Needs:

* Access to telemetry history
* Early identification of anomalies
* Faster troubleshooting

---

### Business Leadership

Responsible for strategic decisions.

Needs:

* Fleet utilization metrics
* Asset performance indicators
* Operational efficiency reporting

---

## Fleet Profile

The company currently supports approximately:

* 5,000 pumps
* 1,200 customer sites
* Multiple provinces and rural regions

### Pump Categories

#### RS 5"

Primary use:

* Agricultural irrigation

Characteristics:

* Long operating cycles
* Seasonal demand

Fleet distribution:

* 60%

---

#### AC 4"

Primary use:

* Livestock watering
* Water transfer

Characteristics:

* Frequent start-stop cycles

Fleet distribution:

* 25%

---

#### AC 6"

Primary use:

* Mobile pumping units
* Emergency response
* Industrial operations

Characteristics:

* Critical availability
* Lower utilization frequency

Fleet distribution:

* 15%

---

# Functional Requirements

The platform must:

FR-01

Receive telemetry from distributed pumps.

FR-02

Store raw telemetry data.

FR-03

Support historical data retention.

FR-04

Provide analytics-ready datasets.

FR-05

Support querying through Amazon Athena.

FR-06

Allow future integration with monitoring and alerting systems.

FR-07

Support schema evolution.

FR-08

Track pump operational status.

---

# Non-Functional Requirements

NFR-01

Serverless-first architecture.

NFR-02

High durability for stored data.

NFR-03

Low operational overhead.

NFR-04

Cost-efficient analytical storage.

NFR-05

Infrastructure managed through Terraform.

NFR-06

Scalable to millions of telemetry records per day.

NFR-07

Secure device communication.

NFR-08

Support intermittent connectivity.

---

# Telemetry Frequency

Each pump publishes telemetry every minute.

Expected volume:

5,000 pumps × 1 event/minute

≈ 7.2 million events/day

≈ 216 million events/month

---

# Telemetry Attributes

Each telemetry event contains:

* timestamp
* pump_id
* site_id
* pump_model
* status
* flow_rate_m3h
* pressure_bar
* motor_temperature_c
* vibration_mm_s
* power_kw

---

# Future Enhancements

Out of scope for phase 1:

* Machine learning
* Predictive maintenance
* Generative AI assistants
* Automated alerting
* Real-time dashboards

These capabilities may be implemented in future releases.
