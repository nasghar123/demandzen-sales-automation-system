# demandzen-sales-automation-system

Developer briefing and prototype assets for **DemandZEN** sales automation: pre-call research (**ZENDiscovery**), post-call intelligence (**ZENpost**), and post-discovery follow-up deliverables.

**Repository:** [github.com/nasghar123/demandzen-sales-automation-system](https://github.com/nasghar123/demandzen-sales-automation-system)

---

## What this project is

[DemandZEN](https://demandzen.com) is a B2B appointment-setting company. Account Executives run outbound discovery calls with prospects daily. This system automates the full call lifecycle so reps spend less time on admin and more time selling.

| Phase | Product | Description |
|-------|---------|-------------|
| **Pre-call** | ZENDiscovery Complete | Company research, 251-client matching, contact profiling, pitch positioning |
| **Post-call** | ZENpost | SPICED rubric scoring, coaching notes, Salesforce field prep |
| **Post-call** | Post-discovery follow-up | Branded 6-slide PDF leave-behind + follow-up email (planned) |

**Target integrations:** [Fellow.ai](https://fellow.ai) (calendar, transcripts), web search, LLM pipelines, Salesforce.

---

## Repository structure

```
.
├── 01_Overview/
│   └── Developer_Briefing.docx       # Full technical specification (May 2026)
├── 02_Sample_Data/
│   ├── dz_clients_database.json      # 251 historical DemandZEN clients
│   ├── sample_scored_calls.json      # 6 scored discovery calls (schema reference)
│   └── Sample_ZDC_Output_Arkiva.json # Complete ZENDiscovery output example
├── 03_Apps/
│   ├── ZENpost_Dashboard.html        # Prototype dashboard (single-file app)
│   └── Slide_Option_B_Preview.html   # Post-discovery PDF slide design preview
├── 04_Templates/
│   └── Post_Discovery_Follow_Up_v6.pdf
├── README.md
└── .gitignore
```

---

## Quick start — ZENpost dashboard

No build step required. The dashboard is a self-contained HTML prototype with embedded sample data.

```bash
git clone https://github.com/nasghar123/demandzen-sales-automation-system.git
cd demandzen-sales-automation-system
```

1. Open `03_Apps/ZENpost_Dashboard.html` in Chrome, Edge, or Firefox.
2. Sign in using the demo access code documented in `01_Overview/Developer_Briefing.docx` (prototype only — not for production).
3. Explore **Upcoming Calls**, **Past Calls**, rubric/SPICED tabs, SFDC fields, research modal, and PDF export.

PDF generation uses [html2canvas](https://html2canvas.hertzen.com/) and [jsPDF](https://github.com/parallax/jsPDF) loaded from CDN.

---

## ZENDiscovery Complete (research pipeline)

Given a prospect company URL, the pipeline runs three phases:

1. **Account research** — 15+ web searches (company, funding, news, leadership, ICP, competitors, outbound signals).
2. **Client matching** — Compare against `dz_clients_database.json`; score as DIRECT / ADJACENT / PEER; generate pitch angle and discovery questions.
3. **POC research** — Profile contacts (LinkedIn or calendar data); prior-employment cross-check against DZ clients.

**Output schema (top-level keys):**  
`meta` · `classification` · `company` · `funding` · `product` · `go_to_market` · `competitive_position` · `social_proof` · `news` · `buyer` · `outbound_intelligence` · `leadership` · `client_matches` · `contacts` · `prior_employment` · `dz_positioning` · `cliff_notes`

See `02_Sample_Data/Sample_ZDC_Output_Arkiva.json` for a full example.

---

## ZENpost call scoring rubric

| Category | Weight |
|----------|--------|
| Preparation + Social Proof | 15% |
| SPICED: Situation | 10% |
| SPICED: Pain Probing | 20% |
| Metrics — Sales Math & ICP | 20% |
| SPICED: Impact | 15% |
| SPICED: Critical Event | 10% |
| SPICED: Decision Process | 5% |
| Closing — Confirmed Follow-up | 5% |

**Additional flags:** AE talk time > 55%, competitors mentioned, DZ clients referenced.  
Sample scored calls: `02_Sample_Data/sample_scored_calls.json`.

---

## Production roadmap

| Milestone | Description |
|-----------|-------------|
| Morning pipeline | Fellow API → prospect domain → ZENDiscovery → deliver to AE before call |
| Post-call pipeline | Fellow transcript → rubric scoring → dashboard + SFDC + follow-up assets |
| Hosted web app | Authentication, persistent storage, real-time Fellow sync (replace embedded JSON prototype) |

Full requirements: `01_Overview/Developer_Briefing.docx`.

---

## Development notes

- Use sample JSON files as API contracts when building backend services.
- Do not commit secrets (`.env`, Fellow tokens, production credentials).
- The HTML dashboard is a UX reference; production should use a proper frontend, API, and database.

---

## License

Proprietary — DemandZEN. All rights reserved unless otherwise agreed in writing.
