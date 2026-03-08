# Drift Detection

## What is Thesis Drift?

Thesis drift occurs when the research pipeline's framing gradually shifts without explicit decision — typically caused by:
- Repeated exposure to a dominant narrative in sources
- Survivorship bias in query results
- Implicit confirmation seeking

## Drift Indicators

| Indicator | Threshold | Action |
|-----------|-----------|--------|
| Contradiction queries returning 0 deltas for 10+ runs | Suspicious | Reformulate contradiction queries |
| Single source type > 70% of citations in a run | Over-concentration | Diversify query targets |
| All deltas support same thesis direction | Confirmation bias risk | Explicitly seek disconfirming evidence |
| Systems thread thesis confidence all "High" | Over-certainty | Stress-test each thesis independently |

## Weekly Drift Review Checklist

```
□ Review active thesis list in SYSTEMS_THREAD_SCHEMA.md
□ For each thesis: has contradicting evidence been encountered in past 7 days?
□ Run one explicit contradiction query per thesis
□ Downgrade confidence on any thesis with no new supporting evidence for 14+ days
□ Check source distribution: no single source type > 60%
□ Assess query coverage: any domain with < 1 delta per week → query refresh
```
