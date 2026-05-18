# demandzen-sales-automation-system

Materials for building DemandZEN's sales automation stack: pre-call research (ZENDiscovery), post-call review (ZENpost), and post-discovery follow-up assets.

Repo: https://github.com/nasghar123/demandzen-sales-automation-system

## About

DemandZEN runs outbound BDR programs for B2B clients. Account Executives hold discovery calls every day. This repo holds specs, sample data, and a working HTML prototype so engineering can wire up the real system later.

Pre-call work is ZENDiscovery (company research, client matching, contact notes). After the call, ZENpost scores the conversation and helps prep Salesforce fields. Follow-up is a branded PDF leave-behind (and email draft later).

Planned hooks: Fellow for calendar and transcripts, web search for research, Salesforce for CRM. Details are in the Word doc under `01_Overview`.

## What's in the repo

- `01_Overview/Developer_Briefing.docx` — main spec
- `02_Sample_Data/dz_clients_database.json` — 251 past clients
- `02_Sample_Data/sample_scored_calls.json` — example scored calls
- `02_Sample_Data/Sample_ZDC_Output_Arkiva.json` — full ZENDiscovery JSON example
- `03_Apps/ZENpost_Dashboard.html` — dashboard prototype (open in browser)
- `03_Apps/Slide_Option_B_Preview.html` — slide layout preview
- `04_Templates/Post_Discovery_Follow_Up_v6.pdf` — PDF template

## Run the dashboard

Clone the repo, then open `03_Apps/ZENpost_Dashboard.html` in Chrome or Edge. No install or build step.

Login code is in the developer briefing doc (prototype only). The app loads sample data from inside the HTML file. PDF export pulls html2canvas and jsPDF from a public CDN.

## ZENDiscovery output

Research output is JSON. See `Sample_ZDC_Output_Arkiva.json` for the full shape. Main sections include company profile, funding, product, go-to-market, buyers, news, client matches, contacts, and short cliff notes for the AE.

## Call scoring

Calls are scored against a SPICED-style rubric (prep, situation, pain, metrics, impact, critical event, decision process, close). Weights and examples are in `sample_scored_calls.json` and the briefing doc.

## Next build steps

1. Morning job: pull today's external meetings from Fellow, run ZENDiscovery, send research to the AE.
2. After the call: pull transcript, score, push results to dashboard and SFDC fields.
3. Replace the single HTML file with a hosted app, auth, and a real database.

## Notes for devs

Keep secrets out of git. Treat the JSON samples as the contract for APIs. The HTML file is a UI reference, not the final architecture.

Proprietary: DemandZEN.
