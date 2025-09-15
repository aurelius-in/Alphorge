# Alphorge  

**Agentic venture factory** that goes from **demand signal → deployed software** with minimal human intervention.  

Agents assess market demand, validate with real outreach, auto-build repos (with tests), price/package, launch campaigns, and handle delivery + upsell — with just **one human QA/creative gate** before release. Every decision is logged, evaluated, and cryptographically signed.  

---

## ✨ Core Value  
Alphorge is the first end-to-end **agentic AI product foundry**:  

- **Demand Intelligence** → forecast signals with uncertainty  
- **Opportunity Ranking** → ROI, time-to-MVP, and market fit scoring  
- **Discovery & Outreach** → surveys, cadences, consent flows, call booking  
- **Product Builder** → Cursor-driven codegen patches (FastAPI, DB, LangGraph, React UI, tests, CI)  
- **Release Manager** → CI/CD, changelog, preview URL, HITL approval required  
- **Pricing & Packaging** → tiers, guardrails, WTP testing  
- **Marketing & Sales** → ETA-aware campaigns, assets, CRM integration  
- **Fulfillment & Success** → provisioning, onboarding, telemetry, NPS/upsell  

---

## 🏗 Architecture  

- **Front Door**: Ops console agent + React Studio UI  
- **Orchestration**: LangGraph (Python)  
- **Backend**: FastAPI services; Cursor for iterative codegen patches  
- **Data**: DuckDB/Parquet (experiments/evals), Postgres (ops), S3 (artifacts)  
- **Governance**: OPA/py policy checks, signed append-only audit chain  
- **Observability**: OpenTelemetry traces  
- **HITL gates**: Required for releases, price changes, scaled outreach  

---

## Branding Variants  

<table>
<tr>
<td align="center">
  <img src="docs/media/alphorge_text_ani.gif" alt="Alphorge text animation" width="240"/><br/>
  <sub>Animated Text</sub>
</td>
<td align="center">
  <img src="docs/media/alphorge_icon_ani.gif" alt="Alphorge icon animation" width="180"/><br/>
  <sub>Animated Icon</sub>
</td>
<td align="center">
  <img src="docs/media/alphorge_ani.gif" alt="Alphorge full animation" width="300"/><br/>
  <sub>Icon + Text Animation</sub>
</td>
</tr>
</table>

---

## 📂 Repo Layout

alphorge/ README.md docs/ one-pager.md arch-diagram.png engine/ api/            # FastAPI endpoints graph/          # LangGraph nodes & orchestration policies/       # OPA/py governance checks builders/       # codegen templates evals/          # scenario packs + metrics audits/         # hash-chain utils tests/          # pytest studio/ web/            # React/MUI dashboard (traces, pricing, CRM-lite) flows/            # *.flow.json (Langflow/Visio exports) reports/          # auto-generated eval & decision reports

---

## 🚀 Getting Started  

1. Clone the repo and install dependencies.  
   ```bash
   make dev
   # or
   docker compose up

2. Import a flow from flows/*.flow.json and press Run Scenario.


3. Use POST /build/scaffold to generate a new service scaffold (CRUD + tests + CI + React admin).


4. Review Cursor patches → CI spins a preview URL.


5. Human QA approves release → Marketing & Pricing agents schedule launch → Fulfillment provisions accounts.




---

🔒 Safety & Audit

Outbound outreach uses consent + throttles.

Price guardrails, SBOM checks, and secrets scanning baked in.

Every decision (release, pricing, outreach) is anchored in an append-only signed hash chain.

Policy receipts and OpenTelemetry spans provide traceability across agents.



---

📖 Docs

One-pager

Studio UI

Engine APIs

Flows



---

🧪 API Surface

/opportunities/search → pull signals, forecast demand

/outreach/sequence → send survey / booking cadences

/build/scaffold → generate repo scaffold + tests

/build/patch → apply codegen diffs

/release/prepare → changelog + migrations (requires HITL)

/pricing/suggest → generate guardrailed tiers

/marketing/plan → campaign assets + ETA scheduling

/crm/provision → customer onboarding + telemetry

/trace/{id} → query signed trace

/metrics → demand / build / GTM metrics


---

🗺 Roadmap

30 Days → Core agents wired in LangGraph + Studio UI MVP

60 Days → Outreach consent flows, price guardrails, hash-chain audit

90 Days → Full venture loop: demand → build → launch → telemetry → upsell


---

📜 License

MIT – for research, experimentation, and innovation.
