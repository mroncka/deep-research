# Signal Quality Rubric

## Per-Run Scoring

Score each run on two dimensions:

### Delta Count
| Score | Deltas | Assessment |
|-------|--------|-----------|
| A | 6–10 | Exceptional sweep |
| B | 3–5 | Good sweep |
| C | 1–2 | Thin — query refresh recommended |
| F | 0 | Stale — queries need full rotation |

### Delta Quality
For each delta, score:

| Dimension | 1 (Poor) | 3 (Good) | 5 (Excellent) |
|-----------|----------|----------|---------------|
| **Novelty** | Already in KG | Extends existing node | Creates new node/edge |
| **Source tier** | Single community post | Corroborated secondary | Primary documentation |
| **Predictive value** | Descriptive only | Implies near-term change | Specific testable prediction |
| **Substrate coverage** | 1 substrate updated | 2 substrates updated | All 3 substrates updated |

### Run Score Formula
```
Run Score = Delta Count Score × avg(Delta Quality scores)
```

## Quality Trend Monitoring

Track 5-run rolling average of delta count. If rolling average drops below 2:
1. Audit query banks for staleness
2. Check if research domain has saturated
3. Consider adding new query domain (e.g., new emerging area)
