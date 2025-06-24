# Weather-Forecast

A modern weather forecast application based on Angular 17, providing real-time weather information and future weather forecast functionality.

## Features

- 🌤️ Real-time weather information display
- 📍 City search and location functionality
- 📅 5-day weather forecast
- 🌡️ Detailed information including temperature, humidity, wind speed
- 📱 Responsive design, mobile-friendly
- 🎨 Modern UI interface

## Tech Stack

- Angular 17
- TypeScript
- SCSS
- Angular Material (optional)
- **Open-Meteo API** (Free weather API, no API key required)

## 🌤️ Weather API - Open-Meteo

This project uses **Open-Meteo API**, a completely free weather API that requires no registration or API key.

### Why Open-Meteo?

- ✅ **Completely Free**: No registration, no API key required
- ✅ **No Rate Limits**: No strict calling frequency restrictions
- ✅ **High Quality Data**: Based on ECMWF (European Centre for Medium-Range Weather Forecasts)
- ✅ **Global Coverage**: Supports weather data for any location worldwide
- ✅ **Multiple Languages**: Supports Chinese and English city searches
- ✅ **Real-time Updates**: Data is updated regularly

### API Endpoints

#### 1. Weather Forecast
```
GET https://api.open-meteo.com/v1/forecast
```

**Parameters:**
- `latitude`: Latitude (required)
- `longitude`: Longitude (required)
- `current`: Current weather parameters
- `hourly`: Hourly forecast parameters
- `daily`: Daily forecast parameters
- `timezone`: Timezone (optional)
- `forecast_days`: Number of forecast days (1-16)

#### 2. Geocoding (City Search)
```
GET https://geocoding-api.open-meteo.com/v1/search
```

**Parameters:**
- `name`: City name (required)
- `count`: Number of results to return (optional)
- `language`: Language (zh/en)
- `format`: Response format (json)

### Usage Examples

#### Get Current Weather
```typescript
// Get current weather for Beijing
const url = 'https://api.open-meteo.com/v1/forecast?latitude=39.9042&longitude=116.4074&current=temperature_2m,weather_code,relative_humidity_2m';
```

#### Get 7-Day Forecast
```typescript
// Get 7-day forecast for Beijing
const url = 'https://api.open-meteo.com/v1/forecast?latitude=39.9042&longitude=116.4074&daily=temperature_2m_max,temperature_2m_min,weather_code&forecast_days=7';
```

#### Search for Cities
```typescript
// Search for cities with "Beijing" in the name
const url = 'https://geocoding-api.open-meteo.com/v1/search?name=Beijing&count=5&language=en';
```

#### Complete Weather Data Example
```typescript
// Get comprehensive weather data including current, hourly, and daily forecasts
const url = 'https://api.open-meteo.com/v1/forecast?' + 
  'latitude=39.9042&' +
  'longitude=116.4074&' +
  'current=temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,rain,showers,snowfall,weather_code,cloud_cover,pressure_msl,surface_pressure,wind_speed_10m,wind_direction_10m,wind_gusts_10m&' +
  'hourly=temperature_2m,relative_humidity_2m,apparent_temperature,precipitation_probability,precipitation,rain,showers,snowfall,weather_code,cloud_cover,pressure_msl,surface_pressure,wind_speed_10m,wind_direction_10m,wind_gusts_10m,uv_index,uv_index_clear_sky,is_day&' +
  'daily=weather_code,temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min,precipitation_sum,rain_sum,showers_sum,snowfall_sum,precipitation_hours,precipitation_probability_max,wind_speed_10m_max,wind_gusts_10m_max,wind_direction_10m_dominant,shortwave_radiation_sum,et0_fao_evapotranspiration,uv_index_max,uv_index_clear_sky_max,sunrise,sunset&' +
  'timezone=auto&' +
  'forecast_days=7';
```

#### JavaScript Fetch Example
The typical weather application workflow involves **two main API calls**:

#### Step 1: City Search (Geocoding)
First, convert a city name to coordinates using the geocoding API:

```javascript
// Search for city coordinates
const geocodingUrl = `https://geocoding-api.open-meteo.com/v1/search?name=${cityName}&count=5&language=en`;
```

**Example Response:**
```json
{
  "results": [
    {
      "id": 1816670,
      "name": "Beijing",
      "latitude": 39.9042,
      "longitude": 116.4074,
      "elevation": 43.0,
      "feature_code": "PPLA",
      "country_code": "CN",
      "admin1_id": 1158811,
      "admin2_id": 1158825,
      "admin3_id": 1158826,
      "admin4_id": 1158827,
      "timezone": "Asia/Shanghai",
      "population": 21540000,
      "postcodes": ["100000"],
      "country_id": 1814991,
      "country": "China",
      "admin1": "Beijing",
      "admin2": "Beijing",
      "admin3": "Beijing",
      "admin4": "Beijing"
    }
  ],
  "generationtime_ms": 1.0
}
```

#### Step 2: Weather Data Retrieval
Then, use the coordinates to fetch weather data:

```javascript
// Get weather data using coordinates
const weatherUrl = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,weather_code,relative_humidity_2m&hourly=temperature_2m&daily=temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min,windspeed_10m_max,weather_code&forecast_days=7&timezone=auto`;
```

**Example Response:**
```json
{
  "latitude": 39.875,
  "longitude": 116.375,
  "generationtime_ms": 0.09179115295410156,
  "utc_offset_seconds": 28800,
  "timezone": "Asia/Shanghai",
  "timezone_abbreviation": "GMT+8",
  "elevation": 47.0,
  "current_units": {
    "time": "iso8601",
    "interval": "seconds",
    "temperature_2m": "°C",
    "weather_code": "wmo code",
    "relative_humidity_2m": "%"
  },
  "current": {
    "time": "2025-06-24T22:00",
    "interval": 900,
    "temperature_2m": 30.2,
    "weather_code": 2,
    "relative_humidity_2m": 40
  },
  "hourly_units": {
    "time": "iso8601",
    "temperature_2m": "°C"
  },
  "hourly": {
    "time": [
      "2025-06-24T00:00",
      "2025-06-24T01:00",
      "2025-06-24T02:00",
      "2025-06-24T03:00",
      "2025-06-24T04:00",
      "2025-06-24T05:00",
      "2025-06-24T06:00",
      "2025-06-24T07:00",
      "2025-06-24T08:00",
      "2025-06-24T09:00",
      "2025-06-24T10:00",
      "2025-06-24T11:00",
      "2025-06-24T12:00",
      "2025-06-24T13:00",
      "2025-06-24T14:00",
      "2025-06-24T15:00",
      "2025-06-24T16:00",
      "2025-06-24T17:00",
      "2025-06-24T18:00",
      "2025-06-24T19:00",
      "2025-06-24T20:00",
      "2025-06-24T21:00",
      "2025-06-24T22:00",
      "2025-06-24T23:00"
    ],
    "temperature_2m": [
      27.7, 27.4, 27.3, 25.1, 24.3, 23.9, 24.3, 26.1, 28.7, 30.7,
      32.9, 35.0, 36.8, 38.1, 38.5, 38.6, 38.5, 38.1, 37.4, 35.7,
      33.3, 31.7, 30.2, 28.9
    ]
  },
  "daily_units": {
    "time": "iso8601",
    "temperature_2m_max": "°C",
    "temperature_2m_min": "°C",
    "apparent_temperature_max": "°C",
    "apparent_temperature_min": "°C",
    "windspeed_10m_max": "km/h",
    "weather_code": "wmo code"
  },
  "daily": {
    "time": [
      "2025-06-24",
      "2025-06-25",
      "2025-06-26",
      "2025-06-27",
      "2025-06-28",
      "2025-06-29",
      "2025-06-30"
    ],
    "temperature_2m_max": [
      38.6,
      37.7,
      29.3,
      26.4,
      25.5,
      31.9,
      31.5
    ],
    "temperature_2m_min": [
      23.9,
      23.2,
      23.7,
      21.6,
      21.9,
      21.9,
      25.1
    ],
    "apparent_temperature_max": [
      41.0,
      39.4,
      30.0,
      28.2,
      29.2,
      34.8,
      37.5
    ],
    "apparent_temperature_min": [
      26.9,
      25.5,
      25.5,
      24.6,
      25.3,
      24.9,
      30.6
    ],
    "windspeed_10m_max": [
      9.7,
      13.3,
      18.2,
      8.0,
      6.3,
      9.5,
      7.8
    ],
    "weather_code": [
      3,
      3,
      61,
      61,
      61,
      95,
      96
    ]
  }
}

### Data Field Explanations

#### Basic Information
- **latitude**: Latitude (39.875°N)
- **longitude**: Longitude (116.375°E) 
- **generationtime_ms**: API response generation time (0.091 seconds)
- **utc_offset_seconds**: UTC timezone offset (28800 seconds = +8 hours)
- **timezone**: Timezone name ("Asia/Shanghai")
- **timezone_abbreviation**: Timezone abbreviation ("GMT+8")
- **elevation**: Elevation above sea level (47.0 meters)

#### Current Weather (current)
- **time**: Current time ("2025-06-24T22:00")
- **interval**: Data update interval (900 seconds = 15 minutes)
- **temperature_2m**: Temperature at 2 meters height (30.2°C)
- **weather_code**: Weather code (2 = Partly cloudy)
- **relative_humidity_2m**: Relative humidity at 2 meters height (40%)

#### Hourly Forecast (hourly)
- **time**: 24-hour time array (one data point per hour)
- **temperature_2m**: Corresponding temperature array for each hour
  - Example: 27.7°C (00:00), 27.4°C (01:00), 27.3°C (02:00)...
  - Maximum temperature: 38.6°C (15:00)
  - Minimum temperature: 23.9°C (05:00)

#### Daily Forecast (daily)
- **time**: 7-day date array
- **temperature_2m_max**: Daily maximum temperature
  - June 24: 38.6°C
  - June 25: 37.7°C
  - June 26: 29.3°C
  - June 27: 26.4°C
  - June 28: 25.5°C
  - June 29: 31.9°C
  - June 30: 31.5°C

- **temperature_2m_min**: Daily minimum temperature
  - June 24: 23.9°C
  - June 25: 23.2°C
  - June 26: 23.7°C
  - June 27: 21.6°C
  - June 28: 21.9°C
  - June 29: 21.9°C
  - June 30: 25.1°C

- **apparent_temperature_max**: Daily maximum apparent temperature (feels like)
  - June 24: 41.0°C
  - June 25: 39.4°C
  - June 26: 30.0°C
  - June 27: 28.2°C
  - June 28: 29.2°C
  - June 29: 34.8°C
  - June 30: 37.5°C

- **apparent_temperature_min**: Daily minimum apparent temperature (feels like)
  - June 24: 26.9°C
  - June 25: 25.5°C
  - June 26: 25.5°C
  - June 27: 24.6°C
  - June 28: 25.3°C
  - June 29: 24.9°C
  - June 30: 30.6°C

- **windspeed_10m_max**: Daily maximum wind speed at 10 meters
  - June 24: 9.7 km/h
  - June 25: 13.3 km/h
  - June 26: 18.2 km/h
  - June 27: 8.0 km/h
  - June 28: 6.3 km/h
  - June 29: 9.5 km/h
  - June 30: 7.8 km/h

- **weather_code**: Daily main weather conditions
  - 3: Overcast (June 24-25)
  - 61: Slight rain (June 26-28)
  - 95: Thunderstorm (June 29)
  - 96: Thunderstorm with hail (June 30)

### Weather Icons

Open-Meteo provides free weather icons:
```
https://open-meteo.com/images/weather/day/{weather_code}.svg
https://open-meteo.com/images/weather/night/{weather_code}.svg
```

### Weather Codes

Common weather codes:
- `0`: Clear sky
- `1-3`: Partly cloudy to overcast
- `45, 48`: Fog
- `51-55`: Drizzle
- `61-65`: Rain
- `71-75`: Snow
- `95`: Thunderstorm

### Supported Cities

Open-Meteo supports weather data for:
- All cities in China (Beijing, Shanghai, Guangzhou, Shenzhen, etc.)
- International major cities (New York, London, Tokyo, Paris, etc.)
- Any location worldwide using coordinates
- Fuzzy city name search

## Development Server

Run `ng serve` to start the development server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code Generation

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running Unit Tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## API Documentation

For more detailed information about Open-Meteo API:
- [Open-Meteo Official Website](https://open-meteo.com/)
- [API Documentation](https://open-meteo.com/en/docs)
- [GitHub Repository](https://github.com/open-meteo/open-meteo)

## Screenshots

### 7 Day Forecast & Weather Details

![7 Day Forecast](src/assets/Screenshot2.png)

![Weather Dashboard](src/assets/Screenshot1.png)

