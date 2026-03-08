# Methodology Changelog

Append-only log of methodology decisions and changes.

---

## 2026-03-08 — Initial Repository Creation

**Decision**: Created `deep-research` as a dedicated methodology repository, separate from `agi-research` (live output).

**Rationale**: The pipeline had grown to R132 runs with significant methodology embedded in the task action string. Externalizing the methodology into a structured repository enables:
1. Version-controlled methodology evolution
2. Explicit query bank management
3. Synthesis pattern documentation
4. Evaluation rubrics for research quality
5. Reusable prompt templates

**Structure**: 6 domains (methodology, queries, synthesis, evaluation, pipeline, meta)

**Live output repository**: [mroncka/agi-research](https://github.com/mroncka/agi-research)

---

## 2026-03-08 — Six Research Track Model

**Decision**: Formalized six research tracks (A: Capability, B: Agentic, C: Security, D: Systems, E: Governance, F: Hardware).

**Rationale**: Pipeline had been sweeping these domains implicitly. Making them explicit enables:
- Per-track query freshness monitoring
- Per-track delta count tracking
- Deliberate contradiction seeking per track

---

## 2026-03-08 — Three-Substrate Parallelism Codified

**Decision**: Every delta must update KG + Tools Registry + Systems Thread simultaneously, or explicitly state which substrate(s) it targets and why the others are excluded.

**Rationale**: Prevents substrate divergence where the KG knows something the tools registry doesn't.
