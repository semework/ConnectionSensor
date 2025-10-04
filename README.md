<p align="center">
  <img src="https://github.com/semework/ConnectionSensor/tree/main/assets" alt="ConnectionSensor logo" width="160" />
</p>

# ConnectionSensor

Objective, explainable analytics for 1:1 conversations — with charts, a stick-figure infographic, and a polished PDF report.
**No attraction/personality inference.** Only observable, defensible metrics.

> **Live Demo**: A working version is available at **[www.digitalocean.com/ConnectionSensor](https://www.digitalocean.com/ConnectionSensor)** — try it and share feedback via our LinkedIn pages below!

**Developed by:**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mulugeta%20Semework-blue?logo=linkedin)](https://www.linkedin.com/in/mulugeta-semework-abebe/)  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Andrew%20Igharo-blue?logo=linkedin)](https://www.linkedin.com/in/andrew-igharo/)

## Features
- **Inputs:** Transcript/Turns CSVs (+ optional Nonverbal & Prosody).
- **Metrics:** Talk-time %, turn lengths (avg/median/P90), overlaps/min, latency, open-question ratio, hedge density.
- **Visuals:** Talk-time bar, turn-length histogram, overlap trend, nonverbal rates, **stick-figure infographic**.
- **Reports:** One-page Executive Snapshot + strengths/opportunities + 3 suggestions, exported as **PDF** + **TXT**.
- **Fake-data chatbox:** Generate synthetic interactions → “Analyze Generated Data”.
- **Style learning:** Bootstraps from local folders to match your look:
  - `interaction_starter_kit/*` (sample CSVs)
  - `sample_results/*` (sample PDF, charts)

## Quickstart (Docker – dev)
```bash
git clone git@github.com:semework/ConnectionSensor.git
cd ConnectionSensor
cp .env.example .env  # fill any keys if using Spaces/Redis, else leave local defaults
docker compose up --build
# API → http://localhost:8000/docs
# Web → http://localhost:5173
```

## Folder bootstrap
On startup (or `POST /bootstrap/from-folders`) the app:
1) Loads `./interaction_starter_kit/*.csv` and computes baseline metrics.  
2) Reads `./sample_results/*` to learn phrasing and visual style.  
3) Caches `{starter_metrics, style_profile}` used to render charts/reports.

## API (core)
- `POST /analyze` – multipart CSVs → returns metrics + signed links to charts, infographic, PDF, TXT.
- `POST /render/infographic` – analysis JSON → PNG/SVG infographic.
- `POST /generate/fake-data` – create synthetic CSVs; optional auto-analyze.
- `POST /bootstrap/from-folders` – (re)learn from the local folders.
- `GET /download/:id` – zip of results (PDF/TXT/PNGs/SVG).

## Tech
- **Backend:** FastAPI, Pandas/Numpy, Matplotlib, ReportLab.
- **Frontend:** React + Vite (Chart.js/Recharts).
- **Storage:** Local `./output` in dev, S3/Spaces in prod (signed URLs + TTL cleanup).
- **Queue:** RQ/Redis for heavy jobs (PDF/images).

## Ethics & Safety
- Requires explicit consent.
- Neutral language: “observed”, “in this sample”.
- “What we do **not** infer” statement on every report.
- Redaction tools for names/locations.

## Deploy (DigitalOcean App Platform)
- 3 components (api, worker, web) + Spaces + Redis add-on.  
- Or a single Droplet with Docker Compose + Nginx TLS.
- Health check `/healthz` warms up plotting backends to avoid first-request lag.

## Contributing
PRs welcome. Please add unit tests for new metrics and snapshot tests for charts/infographic.

## License
Your preferred license here.

---

## Push your local files to GitHub

Use these commands if you already have the `ConnectionSensor` folder locally and want to publish it to **git@github.com:semework/ConnectionSensor.git**:

```bash
cd /path/to/ConnectionSensor

# If this directory is NOT a git repo yet:
git init
git add -A
git commit -m "Initial commit: ConnectionSensor"

# Set the remote (SSH)
git remote add origin git@github.com:semework/ConnectionSensor.git

# Make sure the default branch is main
git branch -M main

# Push
git push -u origin main
```

If a remote already exists and you just want to replace it:
```bash
git remote set-url origin git@github.com:semework/ConnectionSensor.git
git push -u origin main
```
