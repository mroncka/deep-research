# Key Methodology Decisions

Structured record of significant methodology choices, their rationale, and alternatives considered.

---

## D-001: Append-Only Semantics

**Decision**: Living artifacts (KG, Tools Registry, Systems Thread) are append-only. Nodes are updated, not replaced. History is preserved.

**Rationale**: Research value compounds. The trajectory of a finding (when it appeared, how confidence evolved, what it replaced) is as valuable as the current state.

**Alternative considered**: Replace-on-update (simpler, smaller files). Rejected because it destroys the research audit trail.

**Implication**: Files grow monotonically. Monitor KG size — at >2MB, consider archiving old runs to `archive/` and maintaining a current-state summary.

---

## D-002: GitHub as Knowledge Store

**Decision**: Use GitHub as the primary knowledge store, not a vector database or structured DB.

**Rationale**: 
- Git versioning = free temporal audit trail
- Markdown = human-readable + LLM-processable
- GitHub API = accessible from any execution environment
- No infrastructure cost or maintenance

**Alternative considered**: Postgres (structured, queryable). Rejected at current scale — markdown is sufficient and more portable.

**Implication**: At very large scale (KG > 10MB), query performance degrades. If needed, introduce a summary layer that the pipeline reads, with full history archived.

---

## D-003: 30-Minute Cadence

**Decision**: Pipeline runs every 30 minutes.

**Rationale**: Balances freshness against noise. Sub-30min cadence would require significant query rotation to avoid duplicate results. Daily cadence misses fast-moving developments.

**Implication**: ~48 runs/day = ~1440 runs/month. File growth rate: ~10–15KB per run across all artifacts. Monthly KG growth: ~500KB–750KB.

---

## D-004: No Raw GitHub URLs in Sandbox

**Decision**: Never use `raw.githubusercontent.com` URLs in COMPOSIO_REMOTE_WORKBENCH to fetch artifact content.

**Rationale**: The sandbox cannot reach raw GitHub URLs (returns 404). This was discovered empirically at Run ~50 and is a hard constraint.

**Correct method**: `GITHUB_GET_REPOSITORY_CONTENT` → base64 content → decode in workbench.

**Implication**: All artifact fetch steps must use the GitHub API, not raw URLs.

---

## D-005: Proactive Digest vs. Immediate Notification

**Decision**: Pipeline runs are deferred to the daily evening digest (18:00 CET) unless a CRITICAL security event is found.

**Rationale**: 48 daily runs would generate unmanageable notification volume. The digest condenses the day's findings into a single high-signal briefing.

**Exception**: CVE with CVSS ≥ 9.0 affecting a system in active use → immediate notification.
