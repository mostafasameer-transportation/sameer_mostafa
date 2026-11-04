# Website analytics setup

The portfolio dashboard uses GoatCounter for traffic measurement and a scheduled GitHub Actions workflow to publish an aggregated, public snapshot. The API token is stored only as a GitHub Actions secret and is never sent to visitors' browsers.

## 1. Create a GoatCounter site

1. Create a site at https://www.goatcounter.com/ and add the portfolio URL: https://mostafasameer-transportation.github.io/sameer_mostafa/
2. Choose a GoatCounter site code. The hosted statistics address will look like `https://YOUR_CODE.goatcounter.com/`.
3. In GoatCounter, create an API token with read access to statistics.

## 2. Enable tracking in index.html

Replace `YOUR_SITE_CODE` in the GoatCounter tracking script with the actual site code. The tracking script is intentionally not active until this is configured.

## 3. Add GitHub Actions secrets

In the repository, open **Settings → Secrets and variables → Actions → New repository secret** and add:

- `GOATCOUNTER_SITE_CODE`: the site code only, without the domain.
- `GOATCOUNTER_API_TOKEN`: the API token from GoatCounter.

Do not put the API token in `index.html`, a public JSON file, or any client-side JavaScript.

## 4. Run the workflow

Open **Actions → Refresh public website analytics → Run workflow**. The workflow also runs once daily. It writes aggregated counts and country-level totals to `analytics.json`, which the public dashboard reads.

The country breakdown is approximate and represents the last 30 days. The all-time counter starts when GoatCounter tracking is activated. Until the account and secrets are configured, the dashboard intentionally shows no fabricated statistics.
