ADR-001 – Fleet Model Selection
Status

Accepted

Context

The company manufactures multiple centrifugal pump families used across agricultural, industrial, and emergency response scenarios.

For the purpose of this project, a representative subset of the installed base is required to simulate realistic telemetry generation and operational monitoring.

The selected models should:

Represent the most common customer use cases
Reflect real-world operational conditions
Cover different operational profiles
Support meaningful analytical scenarios
Decision

The simulation will use three pump families:

RS 5x5

Primary use:

Agricultural irrigation.

Characteristics:

Long operating cycles
Seasonal demand patterns
Continuous operation during irrigation campaigns
AC 44

Primary use:

Livestock watering systems and water transfer.

Characteristics:

Frequent start-stop cycles
Moderate flow requirements
Distributed deployment across rural locations
AC 66

Primary use:

Mobile pumping units, emergency response systems, and industrial operations.

Characteristics:

Critical availability requirements
Lower operating frequency
High operational impact during failures
Rationale

These models represent the highest-volume product categories and capture the primary operational scenarios encountered by customers.

Using a limited number of representative models reduces simulation complexity while preserving business realism.

Consequences

Benefits:

Realistic telemetry generation
Simplified simulation logic
Easier maintenance
Representative business coverage

Trade-offs:

Less diversity than the complete product catalog
Certain niche operational scenarios are not represented

The architecture remains extensible and additional pump families may be incorporated in future versions.
