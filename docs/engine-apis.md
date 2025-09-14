# Alphorge Flows

Visual exports and runnable configs for LangGraph/Langflow/“Visio”-style diagrams.

## Flow Types
- `demand.flow.json` – signals → forecast → rank
- `build.flow.json` – scaffold → tests → patch review
- `release.flow.json` – prepare → HITL → ship
- `gtm.flow.json` – pricing → marketing → outreach
- `success.flow.json` – provision → telemetry → upsell

## JSON Schema (simplified)
```json
{
  "id": "build.flow",
  "nodes": [
    {"id":"signals","type":"py","fn":"agents.demand.collect"},
    {"id":"forecast","type":"py","fn":"agents.demand.forecast"},
    {"id":"rank","type":"py","fn":"agents.rank.score"},
    {"id":"scaffold","type":"py","fn":"agents.builder.scaffold"},
    {"id":"tests","type":"py","fn":"agents.builder.run_tests"},
    {"id":"hitl","type":"gate","policy":"require_release_approval"},
    {"id":"ship","type":"py","fn":"agents.release.ship"}
  ],
  "edges": [
    ["signals","forecast"], ["forecast","rank"],
    ["rank","scaffold"], ["scaffold","tests"],
    ["tests","hitl"], ["hitl","ship"]
  ]
}
```

Running a Flow

1. Place a *.flow.json in /flows.
2. Start the engine: make dev or docker compose up.
3. From Studio: Flows → Import → Run Scenario.
4. Inspect spans in Traces and policy receipts in the decision detail panel.



Conventions

Every node emits { payload, trace_id, receipts[] }.
Gates must assert policy receipts (OPA) before advancing.
Long-running tasks enqueue jobs and stream updates via Server-Sent Events.
