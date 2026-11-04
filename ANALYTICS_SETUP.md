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

## 4. Run the workflow

Open **Actions → Refresh public website analytics → Run workflow**. The workflow also runs once daily. It writes aggregated counts and country-level totals to `analytics.json`, which the public dashboard reads.

The map places numbered markers at approximate country centroids. GoatCounter reports country-level locations, not precise visitor coordinates. Each marker shows aggregated visits for that country over the reporting period. The all-time counter starts when GoatCounter tracking is activated. Until the API token and repository secrets are configured and the workflow runs successfully, the dashboard intentionally shows no fabricated statistics.
