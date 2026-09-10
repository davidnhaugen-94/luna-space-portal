# Introduction & Overview

Welcome to the official developer reference for the **Luna Space Portal API**. This platform acts as a unified digital gateway, aggregating real-time space data feeds directly from NASA's deep-space telemetries.

By integrating this API, third-party software engineers can instantly pull high-resolution cosmic media files, track passing near-Earth asteroids, and determine whether the northern lights will be visible in a specified location based on the retrieved geomagnetic storm data.

## Core API Infrastructure
The platform is broken down into three core modules:
1.  **Media Services (APOD):** Delivers a daily image, video, or animation of the universe with a descriptive analysis from professional astronomers.
2.  **Northern Lights Forecast (DONKI Systems):** Provides the daily forecast for viewing the northern lights in a specified location. **Note:** This module maps geomagnetic storm data against local weather conditions, requiring developers to integrate a secondary external weather dataset (such as the OpenWeather API).
3.  **Near-Earth Object Tracker:** Computes real-time proximity and sizing telemetry for near-Earth asteroids.

---

## Authentication & Authorization

To protect federal database infrastructure, all client software making calls to the Luna Space Portal must authenticate by passing an API key parameter inside the URL query string using the following authentication pattern:

```http
GET https://api.nasa.gov
```

### Key Management Guidelines
*   **Obtaining Credentials:** Register your development profile on the core application dashboard to retrieve a unique alphanumeric access token.
*   **Security Best Practices:** Never commit your raw API key directly to public code repositories or client-facing scripts. Always inject the token at runtime using an encrypted environment variable.
*   **Rate Limits:** Standard evaluation keys are restricted to a fair-use threshold of **40 requests per hour** or **1,000 requests per day** per individual IP address. Exceeding this limit will trigger temporary server throttling.