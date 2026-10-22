# AtmosFX

**AtmosFX** is a Node.js REST API that combines weather and currency information for cities around the world. It retrieves weather forecasts, identifies a city's country and currency, and provides currency conversion information through external APIs.

## Features

- Retrieve weather information for a city.
- Identify the country and currency associated with a city.
- Retrieve currency exchange rates.
- Compare information for multiple cities.
- Cache data to reduce repeated external API requests.
- Handle invalid requests and external API errors.

## Tech Stack

- **Runtime:** Node.js
- **API:** REST
- **External services:** Open-Meteo, REST Countries, and Frankfurter

## Requirements

- Node.js 20.6 or later
- npm
- An API key for REST Countries only if your implementation or subscription requires one

## Getting Started

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd AtmosFX
```

Replace `<YOUR_REPOSITORY_URL>` with your Git repository URL.

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

If your application requires a REST Countries API key, create a `.env` file in the project root and add:

```env
RESTCOUNTRIES_API_KEY=your_api_key_here
```

Do not commit your actual `.env` file or API keys to GitHub.

If your application does not require an API key, skip this step and remove any unused API-key configuration.

### 4. Start the server

For development, if your `package.json` defines a `dev` script:

```bash
npm run dev
```

Otherwise, use the start command defined in your `package.json`, for example:

```bash
npm start
```

Check the terminal output for the server's local address and port.

## API Endpoints

The following endpoints are documented for the current implementation.

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/health` | Checks whether the API is running |
| `GET` | `/city/:name` | Retrieves weather and currency information for a city |
| `GET` | `/compare?cities=...` | Compares information for multiple cities |

### Health Check

```http
GET /health
```

Checks whether the server is running.

### Get City Information

```http
GET /city/London
```

Retrieves the available weather and currency information for London.

### Compare Cities

```http
GET /compare?cities=London,Tokyo
```

Requests information for multiple cities.

> Endpoint behavior and response fields depend on the current implementation. Check the source code for supported query parameters and error responses.

## Example Response

The following is an illustrative response structure, not a verified live API response:

```json
{
  "city": "London",
  "country": "United Kingdom",
  "currency": "GBP",
  "weather": {
    "temperature": 15,
    "conditions": "Partly cloudy"
  },
  "exchangeRate": {
    "base": "GBP",
    "target": "USD",
    "rate": 1.25
  }
}
```

Actual fields and values may differ depending on your implementation and the data returned by the external services.

## External APIs

AtmosFX uses the following services:

- **Open-Meteo** — city geocoding and weather forecast data: https://open-meteo.com/
- **REST Countries** — country and currency information: https://restcountries.com/
- **Frankfurter** — currency exchange rates: https://frankfurter.dev/

Refer to each service's documentation for its current endpoints, usage limits, and authentication requirements.

## Project Structure

```text
AtmosFX/
├── src/
│   ├── app.js
│   ├── server.js
│   └── services/
│       ├── cache.js
│       ├── city-service.js
│       └── external-api.js
├── .env.example
├── .gitignore
├── LICENSE
├── package.json
├── package-lock.json
└── README.md
```

This structure is illustrative. Keep it aligned with the files and directories in your repository.

## Error Handling

The API should handle common issues such as:

- Unknown or invalid city names
- Missing or invalid query parameters
- External API failures
- Network timeouts
- Rate limits and unavailable services

The exact status codes and error response format depend on the implementation.

## Caching

AtmosFX includes a caching service intended to reduce repeated external API requests. Cache behavior and expiration times are determined by the current configuration.

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

*AtmosFX — weather and currency information through a single API.*