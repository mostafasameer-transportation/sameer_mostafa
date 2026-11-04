# Website analytics setup

The portfolio dashboard uses GoatCounter for traffic measurement and a scheduled GitHub Actions workflow to publish an aggregated, public snapshot. The API token is stored only as a GitHub Actions secret and is never sent to visitors' browsers.

## 1. Create a GoatCounter site

1. Create a site at https://www.goatcounter.com/ and add the portfolio URL: https://mostafasameer-transportation.github.io/sameer_mostafa/
2. Your configured site code is `mostafasameer334`; its hosted statistics address is `https://mostafasameer334.goatcounter.com/`.
3. In GoatCounter, create an API token with read access to statistics.

## 2. Enable tracking in index.html

The tracking script in `index.html` is configured for `mostafasameer334`. After GitHub Pages deploys, visit the portfolio once with content blockers disabled. GoatCounter should begin showing pageviews after it receives the first event.

## 3. Add GitHub Actions secrets

In the repository, open **Settings → Secrets and variables → Actions → New repository secret** and add:

- `GOATCOUNTER_SITE_CODE`: `mostafasameer334`.
- `GOATCOUNTER_API_TOKEN`: the API token from GoatCounter.

Do not put the API token in `index.html`, a public JSON file, or any client-side JavaScript.

## 4. City-level location enrichment and privacy

The site uses IPWho.is from each visitor's browser to estimate the visitor's city, region, country, and approximate coordinates. This sends the visitor's public IP address to IPWho.is for lookup. The site does not request GPS permission and does not collect a street address.

Only the country code, region name, city name, and latitude/longitude rounded to one decimal place are sent to GoatCounter as a custom event. The raw IP address is not written into the event path or the public `analytics.json` file. One city event is recorded per browser tab session. IP-based city estimates can be wrong, especially for VPNs, mobile networks, and corporate networks. The IPWho.is free endpoint has usage limits; if it is unavailable or rate-limited, ordinary country-level analytics continue to work.

The map and analytics panel disclose that city locations are approximate and identify IPWho.is as the lookup provider.

## 5. Run the workflow

Open **Actions → Refresh public website analytics → Run workflow**. The workflow also runs once daily. It writes aggregated counts, country totals, and city-level event totals to `analytics.json`, which the public dashboard reads. The city event data is retrieved from GoatCounter's statistics API and is limited to the reporting window.

The API token remains in GitHub Actions secrets. Never place it in `index.html`, `analytics.json`, or client-side JavaScript. Until the API token and repository secrets are configured and the workflow runs successfully, the dashboard will not show fabricated statistics.
