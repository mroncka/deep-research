# Knowledge Graph Schema

Live artifact: [agi-research/findings/KNOWLEDGE_GRAPH.md](https://github.com/mroncka/agi-research/blob/main/findings/KNOWLEDGE_GRAPH.md)

## Node Types

| Type | Description | Required Fields |
|------|-------------|----------------|
| `MODEL` | AI model/system | name, version, developer, capability_tier, benchmark_scores |
| `FRAMEWORK` | Orchestration/runtime framework | name, version, status, protocol_support, benchmark_rank |
| `PROTOCOL` | Communication/interop standard | name, version, endorsements, adoption_status |
| `CVE` | Security vulnerability | id, severity, affected_systems, patch_status |
| `STANDARD` | Governance/regulatory standard | name, body, timeline, compliance_tier |
| `HARDWARE` | Silicon/infrastructure | name, vendor, specs, availability, agentic_relevance |
| `PHENOMENON` | Systems theory pattern | name, evidence, confidence, alpha_value (if power-law) |
| `EVENT` | Point-in-time occurrence | date, description, significance_tier |
| `ACTOR` | Company/institution/person | name, role, influence_vector |

## Edge Types

| Edge | Source → Target | Description |
|------|----------------|-------------|
| `BUILT_ON` | FRAMEWORK → PROTOCOL | Framework implements protocol |
| `COMPETES_WITH` | FRAMEWORK ↔ FRAMEWORK | Direct competitive relationship |
| `SUPERSEDES` | FRAMEWORK → FRAMEWORK | Evolutionary replacement |
| `PATCHES` | CVE → FRAMEWORK | Vulnerability patched in version |
| `ENDORSES` | STANDARD → PROTOCOL | Standard formally endorses protocol |
| `ENABLES` | HARDWARE → MODEL | Hardware unlocks capability tier |
| `EXHIBITS` | SYSTEM → PHENOMENON | System demonstrates emergence pattern |
| `ACQUIRED_BY` | ACTOR → ACTOR | Corporate acquisition |
| `GOVERNS` | STANDARD → MODEL/FRAMEWORK | Regulatory scope |

## Confidence Tiers

| Tier | Label | Criteria |
|------|-------|----------|
| 1 | `[CONFIRMED]` | Peer-reviewed or primary documentation |
| 2 | `[CORROBORATED]` | 2+ independent secondary sources |
| 3 | `[REPORTED]` | Single credible source |
| 4 | `[INFERRED]` | Derived from confirmed signals |
| 5 | `[HYPOTHETICAL]` | Forward projection |
