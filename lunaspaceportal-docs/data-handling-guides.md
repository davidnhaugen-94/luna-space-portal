# Data Handling & Metric Specifications

Because the Luna Space Portal API converts complex scientific data streams into human-readable responses, developers must adhere to specific formatting rules to avoid compilation errors.

## Temporal Standards (Dates & Times)
All date queries passed as inputs to this API must conform strictly to the international ISO date layout template:
*   **Format Rule:** `YYYY-MM-DD` (e.g., Year-Month-Day).
*   **Correct Syntax:** `2026-08-28`
*   **Incorrect Syntax:** `08/28/2026` or `August 28, 2026` (Passing non-ISO structures will instantly result in a server parsing fault).

---

## Planetary Telemetry Units
To prevent layout inconsistencies across client apps, sizing metrics are structured into specific scientific measurements.

| Data Property | Primary Unit | Description |
| :--- | :--- | :--- |
| `estimated_diameter` | Meters (`m`) | Used to evaluate the physical size of near-Earth asteroids. |
| `relative_velocity` | Kilometers per Hour (`km/h`) | Represents the velocity of tracking objects relative to Earth. |
| `miss_distance` | Kilometers (`km`) | Indicates proximity distance.|

---

## Understanding Hazard Classification Flags
The system handles a boolean attribute labeled `is_potentially_hazardous_asteroid`. A space rock is flagged as `true` if it meets two exact criteria evaluated by automated radar stations:
1.  **Proximity Approach:** Its minimum orbit intersection distance from Earth is less than **0.05 astronomical units** (roughly 7.5 million kilometers).
2.  **Physical Sizing:** The object possesses an absolute brightness index suggesting its diameter exceeds roughly **150 meters** in width.