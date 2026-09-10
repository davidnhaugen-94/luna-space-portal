# Data Handling & Metric Specifications

Because the Luna Space Portal API converts complex scientific data streams into human-readable responses, developers must adhere to specific formatting rules to avoid compilation errors.

## Temporal Standards (Dates & Times)
All date queries passed as inputs to this API must conform strictly to the international ISO date layout template:
*   **Format Rule:** `YYYY-MM-DD` (e.g., Year-Month-Day).
*   **Correct Syntax:** `2026-08-28`
*   **Incorrect Syntax:** `08/28/2026` or `August 28, 2026` (Passing non-ISO structures will instantly result in a server parsing fault).

---

## Understanding Kp Index Measurements
Geomagnetic storms cause the aurora borealis (northern lights) to be visible in the northern hemisphere. The Kp index indicates the intensity of a geomagnetic storm. The higher the intensity, the further south the northern lights may be seen. Below is a table that estimates where in North America the northern lights will be visible depending on the Kp index.

| Kp| Estimated Viewing Area | Example Locations |
| :--- | :--- | :--- |
| `0–2.9` | Far northern Canada & Alaska | Yellowknife, Fairbanks |
| `3.0-3.9` | Northern Canada; far northern U.S. | Northern Minnesota, Maine, Alaska |
| `4.0-4.9` | Canada and northernmost U.S. | Northern Minnesota, Michigan, Maine |
| `5.0-5.9` | Northern U.S. | Northern Michigan, Maine |
| `6.0-6.9` | Northern/mid-northern U.S. | New York, Idaho |
| `7.0-7.9` | Mid-northern U.S. | Illinois, Oregon |
| `8.0-8.9` | Much of the northern/mid U.S. | Northern California, Alabama |
| `9.0-9.9` | Potentially very far south | Florida, Southern Texas |

---

## Required Weather Data
For the current date, the system needs to retrieve the weather conditions for 9:00 PM, 12:00 AM, and 3:00 AM, since the forecast may vary on any given night.

---

## Planetary Telemetry Units
To prevent layout inconsistencies across client apps,  sizing and distance metrics are structured into the specific scientific measurements commonly used by NASA.

| Data Property | Primary Unit | Description |
| :--- | :--- | :--- |
| `estimated_diameter` | Meters (`m`) | Used to evaluate the physical size of near-Earth asteroids. |
| `relative_velocity` | Kilometers per second (`km/s`) | Represents the velocity of tracking objects relative to Earth. |
| `miss_distance` | Kilometers (`km`) | Indicates miss distance.|

---

## Understanding Hazard Classification Flags
The system handles the following two boolean attributes: `is_potentially_hazardous_asteroid` and `is_sentry_object`. 

For `is_potentially_hazardous_asteroid`, an asteroid is flagged as `true` if it meets two exact criteria evaluated by automated radar stations:
1.  **Proximity Approach:** Its minimum orbit intersection distance from Earth is less than **0.05 astronomical units** (roughly 7.5 million kilometers).
2.  **Physical Sizing:** The object possesses an absolute brightness index suggesting its diameter exceeds roughly **150 meters** in width.

