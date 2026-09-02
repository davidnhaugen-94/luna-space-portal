# Error Handling & Troubleshooting Reference

The Luna Space Portal API utilizes standardized HTTP response codes to indicate request success or runtime processing failures. When a request encounters an error, the system outputs an explicit object detailing the block failure context.

## Summary Matrix of Common Codes
*   `200 OK / 201 Created` – The transaction was processed successfully.
*   `400 Bad Request` – Input parameters are missing or broken.
*   `401 Unauthorized` – Authentication security criteria failed.
*   `429 Too Many Requests` – Rate limit threshold was surpassed.
*   `503 Service Unavailable` – Remote server is down or resetting.

---

## Client-Side Failures (4xx)

### 400 Bad Request
*   **Root Cause:** This occurs when query string parameters contain syntax issues, such as an invalid or future date filter.
*   **Resolution:** Audit your date conversion logic to ensure inputs strictly fit the `YYYY-MM-DD` specification layout.

### 401 Unauthorized
*   **Root Cause:** The `api_key` argument is missing from the query string or does not match an active developer profile signature.
*   **Resolution:** Re-verify your access token character-by-character inside your application configuration variables.

---

## Server-Side Failures (5xx)

### 503 Service Unavailable
*   **Root Cause:** Remote tracking equipment or backend databases are experiencing intense network load spikes, data pipeline resets, or scheduled system infrastructure upgrades.
*   **Resiliency Protocol:** This represents a brief, temporary server state. The client software must never launch persistent loop spam requests during a outage window. Implement a systematic **exponential backoff schedule** to pause application attempts for a minimum of 5 minutes before retrying connection handshakes.