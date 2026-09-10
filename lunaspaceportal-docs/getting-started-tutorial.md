# Tutorial: Building a "Cosmic Alert" Dashboard

This step-by-step tutorial walks you through chaining our three core API endpoints together, along with the weather forecast API, to build a functional, real-time widget for amateur astronomers.

## Prerequisites
Before beginning this tutorial, ensure you have:
*   An active, validated **NASA API key** (obtained from api.nasa.gov).
*   An active **OpenWeather API key** (obtained from openweathermap.org).
*   An active workspace tool (like Postman) or a basic frontend application environment to capture data streams.

---

## Step 1: Initialize the Daily Image/Video

Start by fetching the Astronomy Picture of the Day (`https://api.nasa.gov/planetary/apod`) to establish the background media layout of your application dashboard.

*   **Action:** Trigger a standard `GET` request appending your token.
*   **Implementation Note:** Your code should read the returned `media_type` string. If it returns `"image"`, render the asset inside a standard source image tag. If it returns `"video"`, route the payload destination link directly to an embedded iframe media player.

---

## Step 2: Determine Northern Lights Forecast

Next, provide the forecast for viewing the northern lights in a specified location.

*   **Input:** The user's location. 
*   **Action:** Issue a request to the `https://api.nasa.gov/DONKI/GST` geomagnetic storm monitoring engine and the `https://api.openweathermap.org/data/2.5` weather API to get the local weather forecast. Retrieve the `dt_txt` and `weather` data for 9:00 PM, 12:00 AM, and 3:00 AM.
*   **Dashboard Layout:** Inform users whether the northern lights will be visible tonight (at 9:00 PM, 12:00 AM, and 3:00 AM) in the specified location. Indicate whether it is because of the lack of geomagnetic activity or because of the user's location (cloud cover or geomagnetic activity is not intense enough).

---

## Step 3: Query for Near-Earth Asteroids

Lastly, secure real-time radar data for local objects passing close to Earth's orbital plane within a targeted calendar window.

*   **Action:** Query the `https://api.nasa.gov/neo/rest/v1/feed` endpoint.
*   **Filtering Logic:** Your client software must loop through the returned date array to retrieve each near-Earth asteroid. For each tracked object, configure a UI warning flag that changes to red if the `is_potentially_hazardous_asteroid` property equals `true`.