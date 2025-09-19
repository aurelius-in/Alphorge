<td align="center">
  <img src="docs/media/alphorge_text_ani.gif" alt="Alphorge text animation" width="400"/><br/>
</td>

**Pronounced:** “ALF-forj”

#### Autopilot you can audit. ALPHORGE watches your tools, follows your rules, takes safe actions, and leaves signed proof for every step.

<table>
<tr>
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

## What ALPHORGE means

* **Alpha** = first, best, signal, the earliest event that starts a workflow.
* **Forge** = craft, shape, harden, ship to production with confidence.
* **Together** = a place where first-rate signals are forged into safe actions and trustworthy receipts.

## Layman’s description

ALPHORGE connects to the tools you already use. It watches for alerts, tickets, sensor events, order disputes, and access changes. It checks simple rules you set, does the routine steps for you, and asks a person when something looks unusual. Every action it takes is recorded with a clear receipt that shows what happened, why it was allowed, and when it ran.

## Technical description (at a glance)

* **Core:** multi-agent orchestration that gathers evidence, reasons over policies, chooses actions, and emits signed receipts.
* **Policy:** OPA/Rego policies with risk tiers (low → auto, medium → review, high → escalate).
* **Receipts:** dual format (JSON for systems, PDF for auditors) with cryptographic signatures and hash chain for tamper-evidence.
* **Integrations:** Jira/ServiceNow, Slack/Teams, Okta, GitHub/GitLab, AWS/GCP/Azure, Splunk/Elastic, Stripe/Adyen/PayPal, Shopify/Amazon SP-API, OPC-UA/MQTT for plant signals.
* **Human-in-the-loop:** review queue with compact diffs, reason traces, and one-click approve/decline.

---

## Modules

1. **Controls Autopilot** — IT, Security, GRC
   Access recerts, change-control checks, break-glass audits, least-privilege drift cleanup.

2. **Disputes Mesh** — Payments, CX Ops
   Evidence collection and draft dispositions for chargebacks and marketplace disputes.

3. **CAPA Ops** — Plant, Quality, HSE
   Incident to corrective action. Assign, verify from real telemetry, close with audit pack.

4. **Release & Change Guardrails** — SRE, Platform
   Links code changes to tickets, approvals, and rollout gates with ready-made proof.

All four run on the same platform and share the same policy, agent, and receipt services.

---

## Software stack

**Frontend**

* React + TypeScript, Vite, TanStack Query
* Component kits: Material UI or shadcn/ui
* Auth via OIDC (Okta, Azure AD) using PKCE

**Backend**

* Python 3.11 FastAPI (REST + Webhooks), Uvicorn
* Worker runtime: Celery or Temporal.io (for long-running flows)
* Policy engine: OPA sidecar (Rego)
* Receipt signer: PyHanko (PDF), libsodium (JSON signatures)
* LLM tools: LangChain/LangGraph style orchestration, function/tool calling
* Providers: Azure OpenAI, OpenAI, local gguf via vLLM/llama.cpp (optional)

**Data & infra**

* Postgres (app data) + pgvector (reasoning cache and embeddings)
* Redis (queues, rate limits, locks)
* Object storage: S3 compatible (receipts, evidence packs)
* Observability: OpenTelemetry traces, Prometheus metrics, Grafana dashboards
* Search/logs: Elastic or OpenSearch
* Packaging: Docker, Compose for dev, Helm for K8s
* CI/CD: GitHub Actions with signed artifact attestations (SLSA-friendly)

**Connectors (starter set)**

* Jira, ServiceNow, PagerDuty
* Slack, Microsoft Teams
* Okta, Azure AD, GitHub, GitLab
* AWS, GCP, Azure (IAM, CloudTrail, CloudWatch, GCS/Blob/S3)
* Splunk, Elastic, Datadog
* Stripe, Adyen, PayPal, Shopify, Amazon SP-API
* MQTT/OPC-UA for plant sensors

---

## Flagship use cases

1. **Access recertification and drift cleanup (Controls Autopilot)**

   * **Trigger:** a scheduled recert or an unexpected admin role appears.
   * **Action:** collect who/what/when, check policy, notify manager, stage removal.
   * **Outcome:** remove or downgrade access after approval and store a signed receipt.
   * **KPI:** time to remediate, number of risky roles removed, audit pass rate.

2. **Chargeback response drafting (Disputes Mesh)**

   * **Trigger:** dispute opened for an order.
   * **Action:** pull delivery proof, customer comms, refund history, terms; cite network rules; draft response.
   * **Outcome:** analyst approves and ALPHORGE submits on time with a receipt and win-loss tracking.
   * **KPI:** win rate uplift, cycle-time reduction, avoided write-offs.

3. **Incident to CAPA closure (CAPA Ops)**

   * **Trigger:** safety or quality event from a sensor or operator.
   * **Action:** generate CAPA plan, assign tasks, verify completion from telemetry, produce closure report.
   * **Outcome:** ISO/OSHA-ready audit bundle and a tamper-evident receipt chain.
   * **KPI:** time to containment, CAPA on-time rate, repeat incident reduction.

4. **Release guardrails and change evidence (Release & Change Guardrails)**

   * **Trigger:** PR merge or production change.
   * **Action:** check link to ticket, approvals, test artifacts, SLO risk; gate rollout or canary; post decision.
   * **Outcome:** safe rollout with a complete evidence pack per change.
   * **KPI:** change failure rate, MTTR, audit time saved.

---

## User stories

1. **As an SRE**, I want non-compliant changes to be blocked with a clear reason and a one-click path to fix, so production stays stable and audits are trivial.
   **Acceptance:** when a PR merges without a linked ticket and tests, release is gated, Slack explains the missing items, and a receipt is stored when resolved.

2. **As a Risk Ops analyst**, I want a drafted dispute response with cited rules and all evidence attached, so I can approve quickly and improve win rates.
   **Acceptance:** on dispute creation, a draft with rule citations and attachments is ready within minutes, approval submits automatically, and the outcome updates win-rate analytics.

3. **As a Plant Quality lead**, I want incidents to auto-create a CAPA plan with tasks assigned and verified from real data, so audits pass without manual screenshot hunts.
   **Acceptance:** after an event, tasks are assigned, telemetry closes steps automatically, and the final CAPA bundle is signed and archived.

4. **As a Compliance manager**, I want recurring access reviews to run on schedule with exceptions routed to owners, so we reduce risk and have clean evidence for regulators.
   **Acceptance:** quarterly recerts generate owner-specific queues, actions are approved or auto-remediated per policy, and signed receipts roll up into a report.

---

## How ALPHORGE works (pipeline)

1. **Ingest** → webhooks, schedulers, and connectors pull events.
2. **Enrich** → agents gather missing context (users, assets, orders, sensors).
3. **Decide** → risk tiering + OPA policies choose auto vs review vs escalate.
4. **Act** → run playbooks, call APIs, update tickets, message channels.
5. **Prove** → emit signed receipts; store JSON and PDF; link back to source.
6. **Learn** → human approvals and edits tune patterns within guardrails you set.

---

## Getting started (local dev)

```bash
# 1) Clone and bootstrap
git clone https://github.com/<you>/alphorge.git
cd alphorge

# 2) Dev environment
cp .env.example .env  # fill in local Postgres/Redis and any test API keys

# 3) Start services
docker compose up -d

# 4) Run backend
uvicorn app.main:app --reload --port 8080

# 5) Run web
cd web && npm install && npm run dev
```

**Default services**

* FastAPI on `http://localhost:8080`
* React dev server on `http://localhost:5173`
* Postgres on `localhost:5432`, Redis on `localhost:6379`

---

## Example policy (Rego, very small)

```rego
package alphorge.controls

default risk := "high"

risk = "low" {
  input.control == "access_recert"
  input.role in {"read_only","report_view"}
  input.user.status == "active"
}

require_approval {
  risk != "low"
}
```

---

## Receipt format (JSON sketch)

```json
{
  "id": "rcpt_01J8A7...",
  "timestamp": "2025-09-19T20:15:22Z",
  "actor": "alphorge/controls-autopilot",
  "subject": {"user": "jdoe", "system": "okta"},
  "policy": {"id": "controls/access_recert/v3", "risk": "low"},
  "action": {"type": "role_downgrade", "from": "admin", "to": "developer"},
  "evidence": ["s3://evidence/okta/event-...json", "s3://evidence/ticket-1234.pdf"],
  "signature": {"alg": "Ed25519", "key_id": "signer_prod_v1", "sig": "…"}
}
```

---

## Environment variables (sample)

```
POSTGRES_URL=postgresql://postgres:postgres@localhost:5432/alphorge
REDIS_URL=redis://localhost:6379/0
JWT_ISSUER=https://auth.example.com/
OPA_URL=http://opa:8181
S3_ENDPOINT=http://localhost:9000
S3_BUCKET=alphorge-artifacts
OPENAI_API_KEY=...
AZURE_OPENAI_ENDPOINT=...
```

---

## Security and privacy notes

* Principle of least privilege for all connectors.
* Signed receipts stored in an immutable bucket with lifecycle policies.
* PII redaction and scoped access for reviewers.
* Bring-your-own models and private endpoints supported.

---

## Roadmap hints

* More connectors (Workday, NetSuite, SAP, Snowflake).
* On-prem signing HSM support.
* Policy packs for SOX, ISO 27001, PCI, GMP.
* Evidence graph for cross-case reasoning and duplicate detection.

---

## License

Copyright © 2025 Reliable AI Network, LLC. All rights reserved.
