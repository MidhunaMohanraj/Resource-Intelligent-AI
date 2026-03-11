# Rutomatrix Resource Intelligence AI

> AI-powered internal resource allocation system for Rutomatrix Pvt. Ltd.  
> Find the best team member for any task in seconds — with AI scoring, workload awareness, and external candidate search.

![Stack](https://img.shields.io/badge/Frontend-React%20%2B%20Vite-61DAFB?style=flat-square&logo=react)
![Stack](https://img.shields.io/badge/Backend-Node.js%20%2B%20Express-339933?style=flat-square&logo=node.js)
![Stack](https://img.shields.io/badge/AI-Ollama%20llama3.2-FF6B35?style=flat-square)
![Stack](https://img.shields.io/badge/Scraping-Playwright-2EAD33?style=flat-square)

---

## What It Does

- **Resource Finder** — Describe any task in plain English. AI ranks your team by skill match + workload.
- **External Search** — If no good internal match (score < 75%), search Naukri.com + LinkedIn candidates across India.
- **Team Page** — View all 23 team members, their skills, workload, and active tasks.
- **Projects Page** — 9 live projects with task progress and assigned team members.
- **Task Tracker** — All 37 tasks filterable by status and type.
- **Client Overview** — 6 clients (INTEL, TI, COE, REALTEK, NXP, ZEBRA) with linked projects.
- **Pipeline** — Drag shortlisted candidates through Shortlisted → To Assign → Allocated stages.

---

## Tech Stack

| Layer     | Tech                          |
|-----------|-------------------------------|
| Frontend  | React 18, Vite, plain CSS-in-JS |
| Backend   | Node.js, Express              |
| AI / LLM  | Ollama (llama3.2) — runs locally, free |
| Scraping  | Playwright (Chromium)         |
| Data      | Real company data from Excel files, hardcoded in frontend |

---

## Prerequisites

Before you start, make sure you have:

- [Node.js](https://nodejs.org/) v18 or higher
- [Ollama](https://ollama.com/) installed on your machine
- A terminal (Mac: Terminal or iTerm, Windows: PowerShell or Git Bash)

---

## Setup & Running

You need **3 terminals** open at the same time.

---

### Terminal 1 — Start Ollama (AI Engine)

```bash
ollama serve
```

Then in a separate tab, pull the model (one-time only):

```bash
ollama pull llama3.2
```

> Once downloaded, Ollama runs at `http://localhost:11434`  
> The app works without Ollama too — it falls back to smart keyword-based ranking automatically.

---

### Terminal 2 — Start the Backend

```bash
cd "AI website"/backend
npm install
npx playwright install chromium
npm run dev
```

You should see:
```
✅ Backend running on http://localhost:3001
```

> The backend handles external candidate scraping (Naukri + LinkedIn + Indeed India).  
> If you skip this step, the app still works — external search falls back to demo candidates.

---

### Terminal 3 — Start the Frontend

```bash
cd "AI website"/frontend
npm install
npm run dev
```

You should see:
```
  VITE v5.x  ready in 300ms
  ➜  Local:   http://localhost:5173
```

Open **http://localhost:5173** in your browser.

---

## How to Use

### Finding a Resource

1. Go to **Resource Finder** in the sidebar
2. Describe the task in plain English, e.g.:
   > *"Need someone for AI circuit creation and PCB routing. Python and AI skills required. Low workload preferred."*
3. Optionally pick a **Quick Template** or filter by **Role**
4. Click **Search Internal Team**
5. AI ranks all team members with scores, explanations, and active task info

### External Candidate Search

- If the best internal match scores below 75%, external search unlocks automatically
- Select a location (Bangalore, Hyderabad, Chennai, etc.)
- Click **Search External Candidates**
- Results show from Naukri.com + LinkedIn with profile links

### Shortlisting & Pipeline

- Click **★ Shortlist** on any candidate (internal or external)
- Go to **Pipeline** to move them through stages: Shortlisted → To Assign → Allocated

---

## Project Structure

```
AI website/
├── frontend/
│   ├── src/
│   │   └── App.jsx          # Entire frontend — all pages, data, AI logic
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── backend/
│   ├── server.js            # Express server entry point
│   ├── routes/
│   │   ├── externalSearch.js   # POST /api/external-search/run
│   │   ├── matching.js
│   │   ├── candidates.js
│   │   ├── shortlist.js
│   │   ├── analytics.js
│   │   └── searchRequests.js
│   ├── services/
│   │   └── externalScraper.js  # Playwright scraper (Naukri + LinkedIn + Indeed)
│   ├── db/
│   │   └── schema.sql
│   ├── .env.example
│   └── package.json
│
└── README.md
```

---

## Real Data

All data is sourced from Rutomatrix's internal Excel files:

| File | Contents |
|------|----------|
| Team_details.xlsx | 23 team members with roles, skills, and manager notes |
| Project_details.xlsx | 9 active/upcoming projects |
| Task_details.xlsx | 37 tasks with assignments and status |
| Client_details.xlsx | 6 clients (INTEL, TI, COE, REALTEK, NXP, ZEBRA) |

---

## AI Scoring Logic

Each team member is scored out of 100:

```
Final Score = Skill Match (50%) + Workload/Availability (50%)
```

| Workload Status | Score |
|----------------|-------|
| Available (0 active tasks) | 100% |
| Light Load (1–2 tasks) | 75% |
| Moderate (3–4 tasks) | 50% |
| Heavy Load (5+ tasks) | 25% |

When Ollama is running, the LLM provides nuanced skill-gap analysis and natural language explanations per candidate.

---

## Notes

- **No database needed** — all data is in `App.jsx`
- **External scraping** may return 0 results (Naukri/LinkedIn block automated browsers). The app automatically falls back to demo candidates.
- For **live external scraping**, consider integrating [RapidAPI Jobs API](https://rapidapi.com/search/jobs) (~$20/mo)
- Ollama's `llama3.2` model requires ~2GB disk space and works on Apple Silicon (M1/M2/M3) natively

---

## Built By

**Midhuna** — Rutomatrix Pvt. Ltd.  
AI & Software Team

---
