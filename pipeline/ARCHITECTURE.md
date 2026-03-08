# Pipeline Architecture

## System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    SureThing AI Runtime                      │
│                   (30-min cron trigger)                      │
└──────────────────────────┬──────────────────────────────────┘
                           │
               ┌───────────▼────────────┐
               │   1. State Read         │
               │   pipeline-state.json   │
               │   → run_count, SHA      │
               └───────────┬────────────┘
                           │
          ┌────────────────▼─────────────────┐
          │   2. Parallel Intelligence Sweep  │
          │                                   │
          │  Query A: AGI Breakthroughs        │
          │  Query B: Agentic Systems          │
          │  Query C: Security Threats         │
          │  Query D: Systems Theory           │
          │  Query E: Governance/Policy        │
          │  Query F: Hardware/Infra           │
          │                                   │
          │  + GitHub commit check (parallel) │
          └────────────────┬─────────────────┘
                           │
          ┌────────────────▼─────────────────┐
          │   3. Fetch Living Artifacts        │
          │   (via GitHub API, NOT raw URLs)   │
          │                                   │
          │  KNOWLEDGE_GRAPH.md (base64)       │
          │  TOOLS_REGISTRY.md (base64)        │
          │  SYSTEMS_THEORY_THREAD.md (base64) │
          │  LATEST.md (base64)               │
          └────────────────┬─────────────────┘
                           │
          ┌────────────────▼─────────────────┐
          │   4. Synthesis (REMOTE_WORKBENCH) │
          │                                   │
          │  - Decode base64 artifacts        │
          │  - Validate (not fetch error)     │
          │  - Delta extraction               │
          │  - Triple substrate update        │
          │  - Report generation              │
          │                                   │
          │  Output: /tmp/agi_current/        │
          │    report.md                      │
          │    latest.md                      │
          │    kg_full.md                     │
          │    tools_full.md                  │
          │    sys_full.md                    │
          └────────────────┬─────────────────┘
                           │
          ┌────────────────▼─────────────────┐
          │   5. Atomic GitHub Commit         │
          │   GITHUB_COMMIT_MULTIPLE_FILES    │
          │                                   │
          │  5 files in one commit:           │
          │  - reports/[timestamp]-report.md  │
          │  - findings/LATEST.md             │
          │  - findings/KNOWLEDGE_GRAPH.md    │
          │  - findings/TOOLS_REGISTRY.md     │
          │  - findings/SYSTEMS_THEORY_THREAD │
          └────────────────┬─────────────────┘
                           │
          ┌────────────────▼─────────────────┐
          │   6. State Update                 │
          │   pipeline-state.json             │
          │   → run_count++, new SHA          │
          └──────────────────────────────────┘
```

## Critical Constraints

### Network Constraint (CRITICAL)
- The sandbox (COMPOSIO_REMOTE_WORKBENCH) **CANNOT** reach `raw.githubusercontent.com` — returns 404
- Composio S3 pre-signed URLs expire in ~20 minutes — too short for 30-min pipeline cadence
- **Correct method**: `GITHUB_GET_REPOSITORY_CONTENT` → base64-encoded content → decode in workbench

### Timeout Constraint
- COMPOSIO_REMOTE_WORKBENCH hard timeout: 5 minutes per execution
- KG file can reach 1MB+ — synthesis script must be efficient
- If synthesis is timing out: split into delta extraction (step 1) + substrate update (step 2) scripts

### Atomicity
- All 5 files committed in a single `GITHUB_COMMIT_MULTIPLE_FILES` call
- Prevents partial-write state corruption
- On failure: retry from synthesis step, do not re-run queries

## State File Schema

```json
{
  "run_count": 132,
  "last_run_at": "2026-03-08T22:31:00+01:00",
  "last_commit_sha": "3b9f338d...",
  "files_published": ["2026-03-08-2231-report.md", ...]
}
```
