# Pipeline Runbook

Operational reference for the AGI research pipeline.

## Pre-Run Checklist

```
□ Read pipeline-state.json → extract run_count, last_commit_sha
□ Compute RUN = run_count + 1
□ Compute REPORT_FILENAME = YYYY-MM-DD-HHMM-report.md (Prague time)
□ Set SHA_SHORT = last_commit_sha[:7]
```

## Step 1 — State Read

Read `/cells/[AGI_CELL_ID]/workspace/pipeline-state.json` via Cell filesystem.

Expected fields: `run_count`, `last_run_at`, `last_commit_sha`, `files_published`.

## Step 2 — Parallel Sweep

Fire all 6 web_research queries in parallel. Use query banks from `deep-research/queries/`.

Capture summaries in memory — do not write to disk at this stage.

**Simultaneously**: check for new user commits via `GITHUB_LIST_COMMITS`.

## Step 3 — Fetch Living Artifacts

Fetch via `GITHUB_GET_REPOSITORY_CONTENT` (NOT raw URLs):
- `findings/KNOWLEDGE_GRAPH.md`
- `findings/TOOLS_REGISTRY.md`  
- `findings/SYSTEMS_THEORY_THREAD.md`
- `findings/LATEST.md`

Each returns base64-encoded content. Pass as params to synthesis script.

**Validation**: if decoded content starts with `[FETCH ERROR` or len < 500 chars → use repair script.

## Step 4 — Synthesis

Run synthesis script in COMPOSIO_REMOTE_WORKBENCH.

Script receives via `code_file_params`:
- `kg_b64`: base64 KG content
- `tools_b64`: base64 tools registry content
- `sys_b64`: base64 systems thread content
- `latest_b64`: base64 LATEST.md content
- `run_num`: RUN number
- `timestamp`: Prague ISO timestamp
- `web_research_summaries`: concatenated sweep output

Outputs to `/tmp/agi_current/`: `report.md`, `latest.md`, `kg_full.md`, `tools_full.md`, `sys_full.md`

## Step 5 — Commit

```python
GITHUB_COMMIT_MULTIPLE_FILES(
  owner="mroncka",
  repo="agi-research",
  branch="main",
  message=f"findings: automated intelligence report [run {RUN}] - {DATE}",
  upserts=[
    {"path": f"reports/{REPORT_FILENAME}", "content": report_content},
    {"path": "findings/LATEST.md", "content": latest_content},
    {"path": "findings/KNOWLEDGE_GRAPH.md", "content": kg_content},
    {"path": "findings/TOOLS_REGISTRY.md", "content": tools_content},
    {"path": "findings/SYSTEMS_THEORY_THREAD.md", "content": sys_content},
  ]
)
```

## Step 6 — State Update

Update `pipeline-state.json` with new `run_count`, `last_commit_sha`, `last_run_at`, append to `files_published`.

## Error Recovery

| Error | Action |
|-------|--------|
| Synthesis timeout | Split script into 2 steps: delta extraction → substrate update |
| GitHub 409 on commit | Retry with `max_retries=5` |
| Fetch error on artifact | Use repair script as base, continue |
| web_research returns empty | Log + skip that track, continue with others |
| State file missing | Initialize fresh state: run_count=0 |
