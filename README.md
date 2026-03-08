# deep-research

Systematic methodology for deep AI/AGI research. This repository defines *how* research is conducted — the query architecture, synthesis patterns, evaluation rubrics, and pipeline logic. The live output lives in [agi-research](https://github.com/mroncka/agi-research).

## Repository Map

```
deep-research/
├── README.md                        # This file
├── METHODOLOGY.md                   # Core research philosophy and principles
│
├── queries/                         # Query banks (the intelligence fuel)
│   ├── README.md                    # Query design principles
│   ├── AGI_BREAKTHROUGHS.md         # AGI/capability leap queries
│   ├── AGENTIC_SYSTEMS.md           # Multi-agent, orchestration, runtime queries
│   ├── SECURITY_THREATS.md          # CVE, supply chain, threat model queries
│   ├── SYSTEMS_THEORY.md            # Emergence, phase transition, complexity queries
│   ├── GOVERNANCE_POLICY.md         # Standards, regulation, NIST, compliance queries
│   └── HARDWARE_INFRA.md            # Silicon, inference, edge AI queries
│
├── synthesis/                       # How to turn raw research into structured knowledge
│   ├── README.md                    # Synthesis philosophy
│   ├── DELTA_EXTRACTION.md          # How to extract net-new signal from each run
│   ├── KNOWLEDGE_GRAPH_SCHEMA.md    # Node/edge schema for the living KG
│   ├── TOOLS_REGISTRY_SCHEMA.md     # Schema for the tools/stack registry
│   └── SYSTEMS_THREAD_SCHEMA.md     # Schema for systems theory correlation thread
│
├── evaluation/                      # Signal quality + research health checks
│   ├── README.md                    # Evaluation overview
│   ├── SIGNAL_QUALITY_RUBRIC.md     # How to score research signal quality
│   ├── SOURCE_CREDIBILITY.md        # Source weighting and trust scoring
│   └── DRIFT_DETECTION.md           # Detecting thesis drift or stale assumptions
│
├── pipeline/                        # Automation architecture
│   ├── README.md                    # Pipeline overview
│   ├── ARCHITECTURE.md              # Full pipeline design (query → synthesis → commit)
│   ├── RUNBOOK.md                   # Operational runbook (mirrors agi-research)
│   └── PROMPT_TEMPLATES.md          # LLM prompt templates for synthesis steps
│
└── meta/
    ├── CHANGELOG.md                 # Methodology evolution log
    └── DECISIONS.md                 # Key methodology decisions + rationale
```

## Live Research Output

| Artifact | Location | Updated |
|----------|----------|---------|
| Knowledge Graph | [agi-research/findings/KNOWLEDGE_GRAPH.md](https://github.com/mroncka/agi-research/blob/main/findings/KNOWLEDGE_GRAPH.md) | Every 30 min |
| Tools Registry | [agi-research/findings/TOOLS_REGISTRY.md](https://github.com/mroncka/agi-research/blob/main/findings/TOOLS_REGISTRY.md) | Every 30 min |
| Systems Theory Thread | [agi-research/findings/SYSTEMS_THEORY_THREAD.md](https://github.com/mroncka/agi-research/blob/main/findings/SYSTEMS_THEORY_THREAD.md) | Every 30 min |
| Latest Report | [agi-research/findings/LATEST.md](https://github.com/mroncka/agi-research/blob/main/findings/LATEST.md) | Every 30 min |
| Run Reports | [agi-research/reports/](https://github.com/mroncka/agi-research/tree/main/reports) | Each run |

## Research Stack

- **Runtime**: SureThing AI (30-min cron)
- **Search**: web_research (multi-source synthesis)
- **Storage**: GitHub (append-only, git-versioned)
- **Synthesis**: Extended-reasoning LLM (GPT-5.4 Thinking / Gemini 3.1 Pro)
- **Coordination**: `agi-research` pipeline state (run count, SHA tracking)
