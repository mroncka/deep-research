# Tools Registry Schema

Live artifact: [agi-research/findings/TOOLS_REGISTRY.md](https://github.com/mroncka/agi-research/blob/main/findings/TOOLS_REGISTRY.md)

## Entry Schema

```markdown
### [Tool Name] vX.Y.Z
- **Category**: orchestration | runtime | model | protocol | hardware | security
- **Status**: active | maintenance | deprecated | experimental
- **Stack Fit**: [assessment for production agentic systems]
- **Cost Model**: [pricing / resource cost]
- **Security Posture**: [CVE count, last audit, known issues]
- **Protocol Support**: MCP ✅/❌ | A2A ✅/❌ | AG-UI ✅/❌
- **Benchmark**: [quality score / speed / tokens — cite run]
- **Last Updated**: [run number + date]
- **Notes**: [anything structurally significant]
```

## Stack Fit Ratings

| Rating | Meaning |
|--------|---------|
| `PRODUCTION-READY` | GA, stable API, active maintenance, audit trail |
| `STAGING-READY` | Feature-complete but API may shift |
| `EXPERIMENTAL` | Active development, breaking changes expected |
| `MAINTENANCE-ONLY` | No new features, security patches only |
| `DEPRECATED` | End-of-life, migrate away |

## Security Posture Scoring

| Score | Criteria |
|-------|----------|
| `CLEAN` | No known CVEs, recent audit |
| `PATCHED` | CVEs exist but all patched in current version |
| `ACTIVE-VULNS` | Known unpatched CVEs |
| `CRITICAL` | Remotely exploitable unpatched CVE |
| `UNKNOWN` | No audit data |
