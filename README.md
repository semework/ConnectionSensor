<p align="center">
  <img src="https://github.com/semework/ConnectionSensor/blob/main/assets/connectionsensor_icon.png" alt="ConnectionSensor logo" width="160" />
</p>

# ConnectionSensor

Objective, explainable analytics for 1:1 conversations — with charts, a stick-figure infographic, and a polished PDF report.
**No attraction/personality inference.** Only observable, defensible metrics.

The process is as shown in the image below.<p align="center" style="margin:0;">
  <img
    src="https://github.com/semework/ConnectionSensor/blob/main/assets/about_connection_sensor.png?raw=1"
    alt="ConnectionSensor overview"
    width="100%"
    style="max-width:100%; height:auto; display:block;"
  />
</p>


A one figure sample result looks like the image below.<p align="center" style="margin:0;">
  <img
    src="https://github.com/semework/ConnectionSensor/blob/main/sample_results/interaction.png?raw=1"
    alt="ConnectionSensor overview"
    width="100%"
    style="max-width:100%; height:auto; display:block;"
  />
</p>


**Live Demos:** Try ConnectionSensor here — and share feedback via our LinkedIn pages below!

- **[Firebase](https://studio--studio-9467669221-1774f.us-central1.hosted.app/dashboard)**
- **[DigitalOcean](https://cloud.digitalocean.com/gen-ai/workspaces/11f0a14c-32ec-2f20-b074-4e013e2ddde4/agents/335484b6-a14c-11f0-b074-4e013e2ddde4/playground?i=41bcc9)**



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

## Acknowledgments

ConnectionSensor was conceived and built during the **DigitalOcean NYC Hackathon**.  
Huge thanks to the organizers and community for the energy, mentorship, and feedback:

👉 [DigitalOcean NYC Hackathon – Meetup Event](https://www.meetup.com/digitalocean-newyork/events/311118446/?eventOrigin=group_upcoming_events)

We’re grateful to the volunteers, mentors, and fellow hackers who helped shape the project!
