# Introduction & Overview

Welcome to the official developer reference for the **Luna Space Portal API**. This platform acts as a unified digital gateway, aggregating real-time space data feeds directly from NASA's deep-space telemetries.

By integrating this API, third-party software engineers can instantly pull high-resolution cosmic media files, track passing near-Earth asteroids, and view early warning notifications regarding solar weather anomalies inside a single platform interface.

## Core API Infrastructure
The platform is broken down into three core modules:
1.  **Media Services (APOD):** Delivers daily imagery captured by deep-space sensors alongside descriptive analysis from professional astronomers.
2.  **Planetary Defense (NEO Tracker):** Computes real-time proximity and sizing telemetry for near-Earth asteroids.
3.  **Space Weather (DONKI Systems):** Provides daily data on active Coronal Mass Ejections (CMEs), solar flares, and geomagnetic storms.

---

## Authentication & Authorization

To protect federal database infrastructure, all client software making calls to the Luna Space Portal must authenticate by passing an API key parameter inside the URL query string.

### Authentication Pattern
```http
GET https://nasa.gov
```

### Key Management Guidelines
*   **Obtaining Credentials:** Register your development profile on the core application dashboard to retrieve a unique alphanumeric access token.
*   **Security Best Practices:** Never commit your raw API key directly to public code repositories or client-facing scripts. Always inject the token at runtime using an encrypted environment variable.
*   **Rate Limits:** Standard evaluation keys are restricted to a fair-use threshold of **40 requests per hour** or **1,000 requests per day** per individual IP address. Exceeding this limit will trigger temporary server throttling.