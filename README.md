<div align="center">

# MarketPulse

**Real-time stock analytics for retail investors who want to track what matters — without the noise.**

[![Live Demo](https://img.shields.io/badge/Live_Demo-000000?style=flat&logoColor=60c8f0)](https://drive.google.com/file/d/1fSQ92QuGhAZlmLmUpXLTQo2DphjWP9dQ/view?usp=sharing)
[![GCP](https://img.shields.io/badge/GCP-000000?style=flat&logo=googlecloud&logoColor=60c8f0)](https://cloud.google.com)
[![Node.js](https://img.shields.io/badge/Node.js-000000?style=flat&logo=nodedotjs&logoColor=60c8f0)](https://nodejs.org)

</div>

---

## What it does

MarketPulse lets you build a personal watchlist by adding stock tickers and track their behaviour through real-time interactive charts. Add the stocks you care about, watch price movements update live, and analyse trends — all in one clean dashboard.

No noise. No 47 tabs. Just the stocks you chose, moving in real time.

---

## The user problem

Retail investors tracking multiple stocks typically end up with a mess of browser tabs, delayed price data from free tools, and no clean way to compare movements across a watchlist at a glance. Dedicated platforms like Bloomberg are overkill. Free tools are slow or ad-heavy.

MarketPulse sits in the middle — a focused, fast, personal analytics dashboard built around your specific watchlist.

---

## Product decisions

**Watchlist-first, not market-first**
Most stock dashboards open with market overviews, trending tickers, and news feeds. MarketPulse opens with your watchlist. The assumption is that you already know what you're watching — the product's job is to show you those things clearly, not distract you with everything else.

**Caching to reduce API dependency**
Real-time financial data APIs have rate limits and cost money at scale. The Node.js backend aggregates and caches responses, so repeated requests for the same ticker don't hit the third-party API every time. This keeps the dashboard fast even when multiple charts are updating simultaneously.

**Auto-scaling for traffic spikes**
Stock markets have opening bells and closing bells — usage is predictable but spiky. Deployed on GCP with auto-scaling and load balancing so the dashboard stays responsive during high-traffic moments like market open, without over-provisioning resources the rest of the time.

---

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | React.js · Angular.js |
| Backend | Node.js · REST API |
| Data | FinnHub API · Polygon.io |
| Infrastructure | Google Cloud Platform · Docker |
| Deployment | GCP Cloud Run · Cloud Build |

---

## Architecture overview

```
User watchlist input (ticker symbol)
        ↓
Angular frontend → REST request → Node.js backend
        ↓
Cache check → if miss → FinnHub / Polygon.io API
        ↓
Aggregated response → chart data → Angular chart components
        ↓
GCP Cloud Run (containerised) · auto-scaling · load balanced
```

---

## Running locally

```bash
# Clone the repo
git clone https://github.com/aadhishrii/marketpulse

# Install backend dependencies
cd backend && npm install

# Install frontend dependencies
cd ../frontend && npm install

# Add your API keys
cp .env.example .env
# Add FINNHUB_API_KEY and POLYGON_API_KEY to .env

# Start backend
cd backend && npm start

# Start frontend
cd ../frontend && npm start
```

---

## What's next (V2)

- **Price alerts** — notify when a tracked ticker crosses a threshold you set
- **Portfolio view** — track holdings and overall portfolio performance, not just individual tickers
- **Comparison mode** — overlay two or more tickers on the same chart to compare behaviour
- **Historical range selector** — switch between 1D, 1W, 1M, 1Y views per ticker

---

## Built by

[Aadhishrii Patiil](https://github.com/aadhishrii) — product-minded engineer.
Portfolio · [aadhishrii.hashnode.dev](https://aadhishrii.hashnode.dev)
 
