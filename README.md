# SeaLegs Marine Forecast - OpenClaw Skill

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
  "start_date": "2025-12-05T00:00:00Z",
  "num_days": 2,
  "vessel_info": {"type": "sailboat", "length_ft": 35}  // optional
}
```

**Sample response:**
```json
{
  "id": "spc_MHsijiKNkHdEfsWzrZseMm",
  "coordinates": {
    "latitude": 25.7617,
    "longitude": -80.1918
  },
  "forecast_period": {
    "start_date": "2026-02-09T00:00:00-05:00",
    "end_date": "2026-02-09T23:59:59-05:00",
    "num_days": "1"
  },
  "trip_duration_hours": "8",
  "metadata": {
    "location_name": "Miami Marina"
  },
  "latest_forecast": {
    "status": "completed",
    "ai_analysis": {
      "summary": "Excellent calm conditions all day Monday",
      "daily_classifications": [
        {
          "date": "2026-02-09",
          "classification": "GO",
          "short_summary": "Outstanding conditions all day with very light winds under 7 knots and calm 1.2-1.6 foot seas at comfortable 8-11 second periods. Best window is early morning with near-glassy conditions.",
          "summary": "Outstanding boating conditions throughout Monday with exceptionally light winds and calm seas. Early morning offers the calmest window with 1-5 knot east/northeast winds and smooth 1.1-1.4 foot seas at excellent 9-11 second periods. Mid-morning through afternoon continues excellent with light 3-5 knot northwest to north winds and comfortable 1.4-1.5 foot seas at long 11 second periods."
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
