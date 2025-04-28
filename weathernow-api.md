# WeatherNow API Documentation (fictional)

## Overview

The WeatherNow API provides real-time and forecast weather data for locations worldwide. This RESTful API allows developers to retrieve current conditions, hourly forecasts, and severe weather alerts to integrate into their applications.

**API Version:** v2.1.0  
**Base URL:** `https://api.weathernow.example/v2`  
**Released:** April 2025

## Authentication

WeatherNow API uses API key authentication. Include your API key in the request header:

```
Authorization: Bearer YOUR_API_KEY
```

To obtain an API key, register for a free or paid account at [WeatherNow Developer Portal](https://developers.weathernow.example).

## Rate Limits

| Plan      | Requests per minute | Requests per day |
|-----------|---------------------|------------------|
| Free      | 10                  | 1,000            |
| Basic     | 30                  | 10,000           |
| Premium   | 100                 | 100,000          |
| Enterprise| Custom              | Custom           |

Exceeding rate limits will result in a `429 Too Many Requests` response.

## Endpoints

### Get Current Weather

Retrieves current weather conditions for a specific location.

**Endpoint:** `GET /current`

#### Request Parameters

| Parameter | Type   | Required | Description |
|-----------|--------|----------|-------------|
| lat       | Float  | Yes      | Latitude of the location (-90 to 90) |
| lon       | Float  | Yes      | Longitude of the location (-180 to 180) |
| units     | String | No       | Units of measurement: `metric` (default), `imperial`, or `kelvin` |
| lang      | String | No       | Language code for responses (default: `en`) |

#### Example Request

```bash
curl -X GET "https://api.weathernow.example/v2/current?lat=40.7128&lon=-74.0060&units=imperial" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

#### Example Response

```json
{
  "location": {
    "name": "New York",
    "country": "US",
    "lat": 40.7128,
    "lon": -74.0060,
    "timezone": "America/New_York"
  },
  "current": {
    "time": "2025-04-15T14:30:00-04:00",
    "temp": 72.5,
    "feels_like": 74.1,
    "humidity": 65,
    "wind_speed": 8.5,
    "wind_direction": 220,
    "pressure": 1012,
    "conditions": "Partly Cloudy",
    "icon": "partly_cloudy"
  },
  "meta": {
    "request_id": "f7c3d9a1b2e3",
    "response_time": 0.124
  }
}
```

#### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| location | Object | Information about the requested location |
| location.name | String | City name |
| location.country | String | Country code (ISO 3166-1 alpha-2) |
| location.lat | Float | Latitude coordinate |
| location.lon | Float | Longitude coordinate |
| location.timezone | String | IANA timezone identifier |
| current | Object | Current weather conditions |
| current.time | String | Observation time (ISO 8601 format) |
| current.temp | Float | Temperature in requested units |
| current.feels_like | Float | "Feels like" temperature accounting for humidity and wind |
| current.humidity | Integer | Relative humidity percentage (0-100) |
| current.wind_speed | Float | Wind speed in requested units |
| current.wind_direction | Integer | Wind direction in degrees (0-359) |
| current.pressure | Integer | Atmospheric pressure (hPa) |
| current.conditions | String | Text description of weather conditions |
| current.icon | String | Icon code for weather condition |
| meta | Object | Metadata about the request |
| meta.request_id | String | Unique identifier for this request |
| meta.response_time | Float | Time taken to process the request in seconds |

### Get Forecast

Retrieves weather forecast for the next 5 days with 3-hour intervals.

**Endpoint:** `GET /forecast`

#### Request Parameters

| Parameter | Type   | Required | Description |
|-----------|--------|----------|-------------|
| lat       | Float  | Yes      | Latitude of the location (-90 to 90) |
| lon       | Float  | Yes      | Longitude of the location (-180 to 180) |
| days      | Integer| No       | Number of days to forecast (1-7, default: 5) |
| units     | String | No       | Units of measurement: `metric` (default), `imperial`, or `kelvin` |
| lang      | String | No       | Language code for responses (default: `en`) |

*Note: For brevity, example request and response for this endpoint are omitted in this sample.*

## Error Codes

| Status Code | Description | Possible Cause |
|-------------|-------------|---------------|
| 400 | Bad Request | Invalid parameters provided |
| 401 | Unauthorized | Missing or invalid API key |
| 403 | Forbidden | API key doesn't have access to the requested resource |
| 404 | Not Found | Location data not available |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Server Error | Internal server issue |
| 503 | Service Unavailable | API is temporarily unavailable |

## Error Response Format

```json
{
  "error": {
    "code": 400,
    "message": "Invalid parameters",
    "details": "Parameter 'lat' must be between -90 and 90"
  },
  "meta": {
    "request_id": "a1b2c3d4e5f6"
  }
}
```

## SDK Libraries

WeatherNow provides official client libraries for various programming languages:

- [JavaScript](https://github.com/weathernow/javascript-sdk)
- [Python](https://github.com/weathernow/python-sdk)
- [Java](https://github.com/weathernow/java-sdk)
- [Ruby](https://github.com/weathernow/ruby-sdk)

## Webhooks

Premium and Enterprise users can set up webhooks to receive real-time notifications for severe weather alerts. See our [Webhooks Documentation](https://developers.weathernow.example/webhooks) for details.

## Testing

You can use our sandbox environment for testing:

```
Base URL: https://sandbox.weathernow.example/v2
```

Test API Key: `WEATHER_NOW_TEST_KEY_123456`

The sandbox environment provides simulated data and does not count against your rate limits.

## Additional Resources

- [Getting Started Guide](https://developers.weathernow.example/guides/getting-started)
- [API Changelog](https://developers.weathernow.example/changelog)
- [Community Forum](https://community.weathernow.example)
- [Support Center](https://support.weathernow.example)

## Need Help?

If you have any questions or need assistance, please contact our developer support team at [dev-support@weathernow.example](mailto:dev-support@weathernow.example) or join our [Discord community](https://discord.gg/weathernow).
