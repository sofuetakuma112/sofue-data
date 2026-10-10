# Sofue Data

Daily history for public data that nobody archives.

Sofue Data is a one-person data studio in Japan, run by Takuma Sofue under a sole proprietorship registered in December 2024. Since August 2026 it has recorded public listing data that is overwritten every day, such as App Store charts and company job boards, and published it as data products on the Apify Store. The pipeline is built and maintained with Claude Code.

- Website: https://sofuetakuma.uk
- Contact: hello@sofuetakuma.uk

## Products

| Product | Status | Link |
|---|---|---|
| ATS Hiring Signals: normalized job postings from Greenhouse, Lever, Ashby, SmartRecruiters and Recruitee, with new-role deltas and per-company rollups | Live, free | https://apify.com/tkmvictim/ats-hiring-signals |
| App Store Top Charts: Top Free and Top Paid rankings (up to the top 100) for any storefront | Live, $1 per 1,000 results | https://apify.com/tkmvictim/appstore-history |

## How the data is captured

A Cloudflare Workers cron job runs every two minutes from 06:00 to 08:00 JST and reads one official public endpoint per run, retrying any that fail. Today it covers 20 App Store chart feeds (10 storefronts, Top Free and Top Paid) and the Hacker News front page. Rows are stored in Cloudflare D1 and synced to one NDJSON file per source per day.

## Sample data

[`samples/app-store-us-top-free-2026-10-07.json`](samples/app-store-us-top-free-2026-10-07.json) is one day of the US Top Free chart (100 rows), exactly as recorded. Rankings and app details are as published in Apple's public chart feed.

## Data rules

- Only public listings that app stores and companies publish themselves. No user data, reviews, contact details or private profiles.
- Nothing behind a login, a paid license, or terms that prohibit collection.
- Official JSON endpoints first, with robots.txt respected.
