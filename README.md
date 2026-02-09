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

The API returns an AI-powered marine forecast with safety classifications (GO / CAUTION / NO-GO), detailed weather data, and vessel-specific recommendations.

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

## Weather Data Included

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
