# Tutorial: Building a "Cosmic Alert" Dashboard

This step-by-step tutorial walks you through chaining our three core API endpoints together to build a functional, real-time widget for amateur astronomers.

## Prerequisites
Before beginning this tutorial, ensure you have:
*   A validated development platform API key.
*   An active workspace tool (like Postman) or a basic frontend application environment to capture data streams.

---

## Step 1: Initialize the Daily Image/Video

Start by fetching the Astronomy Picture of the Day (`/planetary/apod`) to establish the background media layout of your application dashboard.

*   **Action:** Trigger a standard `GET` request appending your token.
*   **Implementation Note:** Your code should read the returned `media_type` string. If it returns `"image"`, render the asset inside a standard source image tag. If it returns `"video"`, route the payload destination link directly to an embedded iframe media player.

---

## Step 2: Query for Near-Earth Asteroids

Next, secure real-time radar data for local objects passing close to Earth's orbital plane within a targeted calendar window.

*   **Action:** Query the `/neo/rest/v1/feed` endpoint.
*   **Filtering Logic:** Your client software must loop through the returned date array to retrieve each near-Earth asteroid. For each tracked object, configure a UI warning flag that changes to red if the `is_potentially_hazardous_asteroid` property equals `true`.

---

## Step 3: Query for Solar Weather Data

Lastly, provide the latest solar flare, coronal mass ejection, and magnetic storm information that can to warn users about potential satellite or communication line disruptions.

*   **Action:** Issue a request to the `/DONKI/CME`, `/DONKI/FLR`, and `/DONKI/GST` solar weather monitoring engine.
*   **Dashboard Layout:** For the current day `start_date`, notify users whether any solar weather may affect earth inside a prominent banner at the top of your visual layout.