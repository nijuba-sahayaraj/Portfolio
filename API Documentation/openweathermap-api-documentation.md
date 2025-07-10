# OpenWeatherMap API Documentation

## Introduction

This API documentation provides details about the OpenWeatherMap API, enabling developers to retrieve weather data, forecasts, air pollution levels, and historical weather information.

## Base URL
```
https://api.openweathermap.org/data/2.5
```

## Authentication
This API uses an **API Key** for authentication. You must include your API key in requests as a query parameter:

```
appid=YOUR_API_KEY
```


## Table of Contents

1. [Current Weather Data](#current-weather-data)
2. [5 Day / 3 Hour Forecast](#forecast)
3. [Air Pollution Data](#air-pollution-data)
4. [Historical Weather Data](#historical-weather-data)
5. [One Call API](#one-call-api)
6. [Error Responses](#error-responses)
7. [Rate Limiting](#rate-limiting)

## Current Weather Data

### Get Current Weather by City Name

- **URL:** `/weather`
- **Method:** `GET`
- **Description:** Retrieves current weather data by city name.
- **Query Parameters:**
  - `q`: City name (e.g., `London`)
  - `appid`: Your API key
  - `units`: (optional) `metric`, `imperial`, or `standard`
  - `lang`: (optional) Language code (e.g., `en`, `fr`, `es`)

#### Request:
```
GET /weather?q=London&units=metric&appid=YOUR_API_KEY
```

#### Response:
```json
{
  "coord": { "lon": -0.13, "lat": 51.51 },
  "weather": [{ "main": "Clouds", "description": "broken clouds" }],
  "main": {
    "temp": 18.54,
    "feels_like": 17.86,
    "humidity": 82
  },
  "wind": { "speed": 4.1 },
  "name": "London"
}
```

## Forecast

### 5 Day / 3 Hour Forecast

- **URL:** `/forecast`
- **Method:** `GET`
- **Description:** Get 5-day forecast in 3-hour intervals.
- **Query Parameters:**
  - `q`: City name
  - `appid`: Your API key
  - `units`: (optional) Unit format

#### Request:
```
GET /forecast?q=New York&units=imperial&appid=YOUR_API_KEY
```

#### Response:
```json
{
  "city": { "name": "New York" },
  "list": [
    {
      "dt_txt": "2025-07-10 18:00:00",
      "main": { "temp": 82.4 },
      "weather": [{ "description": "clear sky" }],
      "wind": { "speed": 3.1 }
    }
  ]
}
```

## Air Pollution Data

### Get Air Pollution by Coordinates

- **URL:** `/air_pollution`
- **Method:** `GET`
- **Description:** Returns air quality information for a given location.
- **Query Parameters:**
  - `lat`: Latitude
  - `lon`: Longitude
  - `appid`: Your API key

#### Request:
```
GET /air_pollution?lat=50.04&lon=21.02&appid=YOUR_API_KEY
```

#### Response:
```json
{
  "list": [
    {
      "main": { "aqi": 2 },
      "components": {
        "co": 201.94,
        "pm2_5": 5.52,
        "pm10": 6.45
      }
    }
  ]
}
```

## Historical Weather Data

### Get Historical Weather by Coordinates

- **URL:** `/onecall/timemachine`
- **Method:** `GET`
- **Description:** Fetches historical weather data for a location at a specific time.
- **Query Parameters:**
  - `lat`: Latitude
  - `lon`: Longitude
  - `dt`: UNIX timestamp (UTC)
  - `appid`: Your API key

#### Request:
```
GET /onecall/timemachine?lat=40.71&lon=-74.01&dt=1657046400&appid=YOUR_API_KEY
```

#### Response:
```json
{
  "current": {
    "dt": 1657046400,
    "temp": 23.5,
    "weather": [{ "description": "light rain" }]
  }
}
```

## One Call API

### Consolidated Weather Data

- **URL:** `/onecall`
- **Method:** `GET`
- **Description:** Provides current, minutely, hourly, and daily weather forecasts.
- **Query Parameters:**
  - `lat`: Latitude
  - `lon`: Longitude
  - `exclude`: (optional) Parts to exclude (e.g., `minutely,hourly`)
  - `units`: (optional) Unit format
  - `appid`: Your API key

#### Request:
```
GET /onecall?lat=48.85&lon=2.35&exclude=minutely&appid=YOUR_API_KEY
```

#### Response:
```json
{
  "current": {
    "temp": 26.3,
    "weather": [{ "description": "clear sky" }]
  },
  "daily": [
    { "dt": 1657050000, "temp": { "day": 27.8 }, "weather": [{ "main": "Clear" }] }
  ]
}
```

## Error Responses

| **HTTP Code** | **Error**            | **Description**                                                        |
|---------------|----------------------|------------------------------------------------------------------------|
| 400           | Bad Request           | Missing or incorrect parameters.                                      |
| 401           | Unauthorized          | Invalid or missing API key.                                           |
| 404           | Not Found             | City or endpoint not found.                                           |
| 429           | Too Many Requests     | You exceeded your rate limit.                                         |
| 500           | Internal Server Error | An unexpected error occurred on the server.                           |

### Example Error:
```json
{
  "cod": 404,
  "message": "city not found"
}
```

## Rate Limiting

| **Plan**      | **Limit**                   |
|---------------|-----------------------------|
| Free Plan     | 60 requests/minute          |
| Paid Plans    | Up to 2,000 requests/minute |

### Rate Limit Error Response:
```json
{
  "cod": 429,
  "message": "You have exceeded the rate limit"
}
```
