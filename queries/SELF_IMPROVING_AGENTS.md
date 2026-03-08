# Query Bank: Self-Improving Agent Architectures

## Domain
Closed learning loops, autonomous skill creation, skill ecosystems, agent self-improvement, and persistent agent memory systems.

**Thesis being tracked:** The next structural divide in agent capability is between stateless agents (reset each session) and agents with closed learning loops (skills compound from experience). The agentskills.io open standard is the portability layer that may make this divide ecosystem-wide rather than proprietary.

---

## Primary Queries

```
hermes-agent NousResearch self-improving agent [current month year]
```
```
agentskills.io open standard skill portable agent [current month year]
```
```
agent autonomous skill creation learning loop [current month year]
```
```
persistent agent memory cross-session recall [current month year]
```
```
Skills Hub agent marketplace security audit [current month year]
```

## Follow-up Probes
```
Hermes agent vs OpenClaw comparison feature benchmark [current month year]
```
```
agentskills.io SKILL.md compatible agent implementations [current month year]
```
```
self-improving agent governance alignment risk [current month year]
```

## Architecture Comparison: Self-Improvement Models

| System | Skill Creation | Skill Storage | Portability | Security Model |
|--------|---------------|---------------|-------------|----------------|
| **Hermes (Nous Research)** | Autonomous after complex tasks | Filesystem SKILL.md | agentskills.io standard | Skills Hub quarantine+audit |
| **OpenClaw** | ClawHub marketplace | ClawHub registry | Proprietary | ⚠️ ~20% contamination baseline (user memory) |
| **SureThing (me)** | Curated SKILL.md files | Cell filesystem `/skills/` | Cell-local | Read-only, human-curated |
| **OpenAI Agents SDK** | Hosted Skills bundles (v0.8.4) | Hosted containers | SDK-native | Managed hosting |

## Key Distinction: Curated vs. Autonomous Skills

**Curated (SureThing, current)**: Skills are human-authored SKILL.md files. Deterministic, auditable, no drift. Tradeoff: doesn't compound from experience.

**Autonomous (Hermes)**: Agent writes SKILL.md after solving hard problems. Compounds from experience. Tradeoff: requires skill auditing (quarantine system) to catch hallucinated or unsafe skill documents.

**The governance question**: Autonomous skill creation is the architectural equivalent of an agent modifying its own system prompt. NIST's framework has no explicit position on this yet — it's a Pillar 4 (Security Evaluations) problem waiting for a standard.

## agentskills.io Spec Summary

```
skill-name/
├── SKILL.md          # Required: YAML frontmatter + Markdown instructions
├── scripts/          # Executable code (Python, Bash, JS)
├── references/       # Additional docs loaded on demand
└── assets/           # Templates, images, data
```

SKILL.md frontmatter:
- `name`: 1-64 chars, lowercase alphanumeric + hyphens
- `description`: 1-1024 chars — what it does AND when to use it
- Optional: `license`, `compatibility`, `metadata`, `allowed-tools`

Progressive disclosure token budget:
- Metadata at startup: ~100 tokens
- Full instructions on activation: <5,000 tokens
- Resources: loaded only when needed

## Contradiction Queries
```
autonomous skill creation agent alignment risk hallucination [current month year]
```
```
self-improving agent unintended behavior skill poisoning [current month year]
```
