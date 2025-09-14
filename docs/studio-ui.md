# Alphorge Studio UI

A React + TypeScript dashboard (Vite + MUI) for operating the venture loop.

## Pages / Routes
- **/** – Overview: active opportunities, builds, releases, campaigns, NPS.
- **/signals** – Demand Intelligence: sources, trends, uncertainty bands.
- **/ranker** – Opportunity scoring (ROI, TTMVP, fit) with filters.
- **/builder** – Run `/build/scaffold`, review Cursor patches, test results.
- **/release** – Release Manager: changelog, preview URL, HITL approvals.
- **/pricing** – Tiers, WTP experiments, guardrails.
- **/marketing** – Plans, assets, cadence scheduler, ETA calendar.
- **/crm** – Accounts, provisioning status, telemetry.
- **/traces/:id** – OpenTelemetry & policy receipts for a decision.
- **/settings** – API keys, consent defaults, rate limits.

## State & Data
- **Query**: `@tanstack/react-query`
- **Store**: Zustand (lightweight)
- **API**: `engine/api` (FastAPI), JSON over HTTPS
- **Auth**: Bearer token (env var in dev)

## Components
- **TraceTimeline** – spans + policy receipts
- **PatchReview** – side-by-side code diff, approve/reject
- **UncertaintyChart** – demand forecast with bands (Recharts)
- **GuardrailEditor** – pricing & outreach limits (OPA policy preview)
- **CadenceDesigner** – marketing/outreach steps with consent gates

## Theme
- MUI dark theme
- Primary: #00E676 (logo green), Secondary: #121212, Surface: #1A1D1F

## Dev
```bash
cd studio/web
pnpm i
pnpm dev
# VITE_API_URL=http://localhost:8000
