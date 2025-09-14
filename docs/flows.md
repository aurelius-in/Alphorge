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
