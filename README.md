# Atmos — Weather Dashboard

**Designed for calm, everyday planning.**

Atmos is a responsive weather dashboard built with HTML, CSS, and vanilla JavaScript. It uses the Open-Meteo Forecast API to show current conditions, forecasts, and weather metrics for cities around the world.

## Features

- **Current conditions:** temperature, feels-like temperature, daily high and low, and weather condition.
- **City search:** search a bundled CSV database of nearly 6,000 cities with Fuse.js fuzzy matching.
- **Forecasts:** hourly conditions and precipitation probability, a seven-day outlook, and a daily temperature trend.
- **Weather details:** humidity, wind speed, UV index, visibility, sunrise, sunset, and daylight duration.
- **Temperature units:** switch between Celsius and Fahrenheit.
- **Loading and error states:** a dashboard-shaped skeleton appears while weather loads; an illustrated error state appears when the forecast cannot be retrieved.
- **Favorite cities:** the weather card transforms in place into a favorites view. Each city card opens that city, while its separate remove button deletes it.
- **Responsive glass-style interface:** translucent cards sit above softly animated ambient gradients; layouts adapt to desktop, tablet, and mobile screens.
- **Accessible account links:** the footer includes creator links to GitHub, Instagram, TikTok, Telegram, and WhatsApp.
- **Offline resource caching:** a Service Worker caches core app files and the city database. Weather data still requires an internet connection.
- **Search engine basics:** descriptive page metadata, a crawler access file, and a sitemap for the GitHub Pages URL.

Favorite cities and the selected location are saved in browser storage. If the browser blocks storage, the app keeps changes for the current page session and displays a notice; those changes will not survive closing the page.

### Startup and weather data

The app waits for the Open-Meteo response before rendering weather values. The dashboard-shaped skeleton remains visible while the request is in progress, and the illustrated error state appears if the request fails.

The former `JS/data.js` file held hard-coded sample weather values used to initialize the dashboard. It was removed because those values were not live weather or a reliable offline forecast; showing them could make sample conditions look real. The Service Worker separately caches the app files, while live weather continues to require the API connection.

The default Erbil coordinates match Erbil's entry in the city database, so opening the app and selecting Erbil in search use the same location. Temperature values are displayed directly from Open-Meteo without a fixed manual offset.

## Technology

| Technology | Use |
|---|---|
| HTML5 | Page structure |
| CSS3 | Layout, responsive styling, and animation |
| Vanilla JavaScript | UI behavior, weather data handling, and search |
| Open-Meteo Forecast API | Current weather and forecasts |
| Fuse.js | Fuzzy city search |
| Papa Parse | CSV parsing |
| Meteocons | Weather icons |
| Service Worker | Caching core local resources for offline access |

External resources:

- [Open-Meteo](https://open-meteo.com/)
- [Fuse.js](https://www.fusejs.io/)
- [Papa Parse](https://www.papaparse.com/)
- [Meteocons](https://meteocons.com/)

## Project structure

```text
Atmos/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── data/
│   └── world-cities.csv
├── JS/
│   ├── api.js
│   └── app.js
├── index.html
├── style.css
└── sw.js
```

- `index.html` — Dashboard markup, loading and error screens, and creator links.
- `style.css` — Visual theme, responsive layouts, card styles, and animations.
- `JS/api.js` — Open-Meteo requests, weather data mapping, and saved location handling.
- `JS/app.js` — Search, favorites, unit switching, and dashboard updates.
- `data/world-cities.csv` — Local city database used by search.
- `sw.js` — Service Worker installation, cache versioning, and network-first local resource handling.
- `.github/workflows/deploy.yml` — GitHub Pages deployment workflow.

There is no `data.js`: startup weather is fetched from the API rather than initialized from mock values.

## Run locally

Requirements: a modern browser and a local web server. No package installation or API key is required.

1. Clone or download this repository.
2. Open the project folder in an editor.
3. Start a local server, such as the VS Code Live Server extension.
4. Open the server's local URL in a browser.

Do not open `index.html` using the `file://` protocol. Service Workers require a secure context such as `localhost` or HTTPS.

## Offline behavior

After the Service Worker has installed, core local files and the city database can be served from cache when the network is unavailable. Atmos needs an internet connection to retrieve weather data, so it shows its connection error state instead of stale weather. External libraries and weather icons are hosted separately and may not load offline.

## Weather data attribution

Atmos uses the [Open-Meteo Forecast API](https://open-meteo.com/) for weather data. Open-Meteo data is provided under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

**Weather data by [Open-Meteo.com](https://open-meteo.com/).**

See the [Open-Meteo Terms of Use](https://open-meteo.com/en/terms). The free API is intended for non-commercial use; commercial projects should use an appropriate Open-Meteo subscription.

## Author

**WMJD**

Built as part of a personal web development journey.
