# Delta Extraction

## What Counts as a Delta

A delta is a finding that:
- Does not already exist as a node/entry/correlation in the living artifacts
- Changes the model (not just updates a detail within an existing node)
- Is actionable or predictive

## What Does NOT Count as a Delta

- Version bumps without behavioral change
- Reconfirmation of existing nodes (record as signal depth only)
- Announcements without substance ("Company X is working on Y")
- Benchmark results within margin of error of known state

## Delta Classification

| Class | Description | Substrate Target |
|-------|-------------|------------------|
| `CAPABILITY_LEAP` | Model can now do something it couldn't | KG + Systems |
| `FRAMEWORK_CHANGE` | Structural change to tool/framework | KG + Tools |
| `SECURITY_EVENT` | New CVE, attack, or threat pattern | KG + Tools |
| `GOVERNANCE_MILESTONE` | Standard, policy, or compliance event | KG + Systems |
| `HARDWARE_INFLECTION` | Silicon or infrastructure step-change | KG + Tools |
| `EMERGENCE_SIGNAL` | Collective/complex systems behavior | KG + Systems |
| `MARKET_STRUCTURE` | Company acquisition, pivot, shutdown | KG + Tools |

## Delta Extraction Prompt Template

See `pipeline/PROMPT_TEMPLATES.md` → Section: Delta Extraction
