# Naked Farms · FarmBox

**Software for hydroponic greenhouse farms**

FarmBox is one database and two apps. A single Postgres platform (Supabase, with row-level security) holds the farm's crops, tasks, harvest, climate, pests and costs; a desktop console and a phone app work on the same data, so the office and the crew always see the same farm.

The system proposes, a person validates. The phone app is offline-first: crews keep working in the greenhouse without signal and everything syncs when they are back in range. AI suggestions, from scouting photos to plans, are always proposals that a person reviews before anything changes.

[![Naked Heart](https://img.shields.io/badge/Naked%20Heart-heart.nkd.farm-2e7d32)](https://heart.nkd.farm)
[![Naked Brain](https://img.shields.io/badge/Naked%20Brain-brain.nkd.farm-2e7d32)](https://brain.nkd.farm)

| App | What it is | Live | Repository |
|---|---|---|---|
| **Naked Heart** | Desktop console for managers: planning, operations, costs, team | [heart.nkd.farm](https://heart.nkd.farm) | [Nkdfarm/farmbox-console](https://github.com/Nkdfarm/farmbox-console) |
| **Naked Brain** | Phone PWA for crews: tasks, SOPs, scouting, harvest, voice notes | [brain.nkd.farm](https://brain.nkd.farm) | [Nkdfarm/naked-brain](https://github.com/Nkdfarm/naked-brain) |

## Architecture

```mermaid
flowchart LR
  P[Naked Brain<br/>phone app] --> DB[(Supabase Postgres<br/>row-level security)]
  C[Naked Heart<br/>console] --> DB
  P --> F[Edge functions]
  C --> F
  F --> DB
  CAM[Cameras] --> I[ingest function]
  R[Robot] --> I
  I --> DB
  AI[AI] --> PR[Proposals]
  PR --> V{A person validates}
  V --> DB
```

## Stack

Postgres / Supabase · plain ES-module PWAs · Deno edge functions · Cloudflare · Python for vision and robotics

The platform, vision and robotics work are in private repositories; access on request. More at [nkd.farm](https://nkd.farm).
