# Source Credibility

## Tier System

| Tier | Type | Weight | Examples |
|------|------|--------|----------|
| T1 | Peer-reviewed | 1.0 | arXiv (accepted), Nature, Science, NeurIPS |
| T2 | Primary documentation | 0.9 | Official GitHub releases, company blog (product), NIST docs |
| T3 | Institutional analysis | 0.7 | Gartner, McKinsey, government RFI responses |
| T4 | Corroborated secondary | 0.6 | 2+ independent tech publications |
| T5 | Single secondary | 0.4 | Single tech publication, credible newsletter |
| T6 | Community | 0.2 | HN, Reddit, Discord (useful for trend signals, not facts) |

## Provenance Flags

| Flag | Meaning |
|------|---------|
| `[CHINA-ECOSYSTEM]` | Source from Chinese ecosystem (Track C provenance concern for governed applications) |
| `[SELF-REPORTED]` | Company reporting on own benchmarks (verify independently) |
| `[PREPRINT]` | Not peer-reviewed yet |
| `[COMMUNITY-SIGNAL]` | Useful trend indicator, not factual citation |

## Source Diversity Check

Each run should include sources from at least:
- 1× T1 or T2 (primary)
- 1× academic or institutional
- 1× community (for trend signal)
