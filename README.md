# SeaLegs AI Marine Forecast API - OpenClaw Skill

An OpenClaw skill for getting AI-powered marine weather forecasts via the [SeaLegs API](https://developer.sealegs.ai).

## Features

- **SpotCast Forecasts**: Get marine weather forecasts for any coordinates worldwide
- **AI Safety Analysis**: GO / CAUTION / NO-GO classifications for each day
- **Vessel-Specific**: Tailored recommendations based on boat type and size
- **Multi-Language**: Supports English, Spanish, French, Portuguese, Italian, Japanese

## Quick Start

### 1. Get an API Key

1. Sign up at [developer.sealegs.ai](https://developer.sealegs.ai) — you'll get **10 free credits** to get started
2. Generate an API key
3. Need more? Add credits anytime ($10 = 200 forecast-days)

### 2. Configure OpenClaw

Add to your OpenClaw configuration:

```json5
{
  skills: {
    entries: {
      "sealegs-marine-forecast": {
        enabled: true,
        apiKey: "sk_live_your_key_here"
      }
    }
  }
}
```

Or set the environment variable:

```bash
export SEALEGS_API_KEY=sk_live_your_key_here
```

### 3. Install the Skill

```bash
clawhub install sealegs-marine-forecast
```

## Usage Examples

**Get a forecast for a location:**
```jsonc
// Miami, FL
POST /v3/spotcast
{
  "latitude": 25.7617,
  "longitude": -80.1918,
  "start_date": "2026-02-10T00:00:00Z",
  "num_days": 2,
  "vessel_info": {"type": "sailboat", "length_ft": 35}  // optional
}
```

**Sample response:**
```json
{
  "id": "spc_FrZdSAs6T3cxbXiPtNZvxu",
  "coordinates": {
    "latitude": 25.7617,
    "longitude": -80.1918
  },
  "forecast_period": {
    "start_date": "2026-02-10T00:00:00-05:00",
    "end_date": "2026-02-11T23:59:59-05:00",
    "num_days": "2"
  },
  "trip_duration_hours": "12",
  "metadata": {
    "location_name": "Miami Marina"
  },
  "latest_forecast": {
    "status": "completed",
    "ai_analysis": {
      "summary": "Ideal conditions both days with light winds",
      "daily_classifications": [
        {
          "date": "2026-02-10",
          "classification": "GO",
          "short_summary": "Outstanding conditions all day with light winds under 7kt and calm 1.1-1.6ft seas. Best window is morning 5:00 AM-12:00 PM with nearly calm 1-4kt northwest winds and comfortable 1.4ft seas at 11-second periods.",
          "summary": "Outstanding sailing conditions throughout Monday with exceptionally light winds and calm seas. Morning hours offer the best window with nearly calm 1-4kt northwest winds and comfortable 1.4ft seas at 11-second periods from the northeast."
        },
        {
          "date": "2026-02-11",
          "classification": "GO",
          "short_summary": "Exceptional conditions with very light winds 1-6kt and minimal 1.2-1.3ft seas all day. Best window 9:00 AM-1:00 PM offers glassy conditions with 1-3kt winds and 1.2ft seas at 11-second periods.",
          "summary": "Exceptional boating conditions on Tuesday with very light winds and minimal seas throughout the day. Morning through midday provides ideal glassy conditions with 1-3kt east-southeast winds and 1.2ft seas at 10-11 second periods from the northeast."
        }
      ]
    }
  }
}
```

## API Endpoints

| Operation | Endpoint | Cost |
|-----------|----------|------|
| Create forecast | POST /v3/spotcast | 1 credit/day |
| Get forecast | GET /v3/spotcast/{id} | Free |
| Check status | GET /v3/spotcast/{id}/status | Free |
| Refresh forecast | POST /v3/spotcast/{id}/refresh | 1 credit/day |
| List forecasts for SpotCast | GET /v3/spotcast/{id}/forecasts | Free |
| Get specific forecast | GET /v3/spotcast/{id}/forecast/{forecast_id} | Free |
| List SpotCasts | GET /v3/spotcasts | Free |
| Get balance | GET /v3/account/balance | Free |

## Weather Factors Used

- Wind speed, gusts, and direction
- Wave height, period, and direction
- Visibility and fog probability
- Precipitation probability and intensity
- Air and water temperature

## Links

- [Developer Portal](https://developer.sealegs.ai)
- [API Documentation](https://developer.sealegs.ai/docs/)
- [SeaLegs App](https://sealegs.ai)

## License

MIT
