# Pipeline

The research pipeline is a 30-minute cron automation that:
1. Sweeps all 6 research domains using the query banks
2. Synthesizes net-new deltas via LLM
3. Updates three living artifacts (KG, Tools Registry, Systems Thread)
4. Commits atomically to `agi-research`
5. Updates pipeline state

Full architecture: `ARCHITECTURE.md`  
Operational runbook: `RUNBOOK.md`  
Prompt templates: `PROMPT_TEMPLATES.md`
