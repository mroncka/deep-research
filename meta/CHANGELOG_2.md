# Changelog (continued)

---

## 2026-03-08 — Company Graphs + Hermes/agentskills.io Integration

**Added:**
- `queries/COMPANY_GRAPHS.md` — arscontexta methodology, company graph architecture queries, systems theory connections
- `queries/SELF_IMPROVING_AGENTS.md` — Hermes, agentskills.io, closed learning loops, autonomous skill creation
- `synthesis/COMPANY_GRAPHS_METHODOLOGY.md` — full arscontexta methodology distilled from @arscontexta article (Feb 25, 2026, 356K impressions)
- `synthesis/HERMES_AND_AGENTSKILLS.md` — Hermes architecture analysis, agentskills.io spec, competitive vs. OpenClaw, ARCHIVIST relevance

**Rationale:** Three signals arrived simultaneously pointing at the same structural gap:
1. @arscontexta article "Company Graphs = Context Repository" — the organizational knowledge graph as agent context architecture
2. NousResearch/hermes-agent — closed learning loop + agentskills.io as the skill portability standard
3. User request to incorporate both into the research infrastructure

All three are facets of one thesis: *structured context graphs as the operating surface for agentic systems*. They belong in `deep-research` as methodology, not just as KG nodes in `agi-research`.

**Gap identified:** `agi-research` pipeline uses monolithic markdown blobs (KNOWLEDGE_GRAPH.md at ~865KB). The arscontexta article makes a strong case that atomic wikilinked nodes would be more agent-traversable at scale. This is a future architecture decision, not an immediate change — tracked in `meta/DECISIONS.md`.

**ARCHIVIST connection logged:** Hermes' multi-level memory + subagent RPC + Atropos RL = relevant to harness layer architecture.
