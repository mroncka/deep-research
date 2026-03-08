# Hermes Agent & agentskills.io

**Source:** NousResearch/hermes-agent (GitHub) | agentskills.io
**Relevance:** Direct architectural comparison to this pipeline; OpenClaw ecosystem competitor; ARCHIVIST project context

---

## What Hermes Is

Hermes is Nous Research's open-source self-improving agent runtime. Key distinction from other frameworks:

**It has a closed learning loop.** After solving complex problems, Hermes autonomously creates SKILL.md files documenting its approach. These become searchable procedural memory that the agent reuses when similar tasks arise. Skills self-improve during use.

This is architecturally distinct from every other major agent framework, which are stateless between sessions (or manage state externally). Hermes makes skill accumulation a first-class primitive.

---

## Architecture

**Deployment**: Self-hosted — $5 VPS, Docker, SSH, Daytona, Modal (serverless). Six terminal backends.

**Multi-platform gateway**: Telegram, Discord, Slack, WhatsApp, CLI — all from one gateway process.

**Memory system (multi-level)**:
1. Session memory (in-context)
2. Skill documents (procedural, filesystem)
3. Cross-session FTS5 search with LLM summarization
4. Honcho dialectic user modeling (persistent user profile)

**Parallelization**: Spawns isolated subagents for parallel workstreams. Python scripts call tools via RPC.

**Research infrastructure**: Batch trajectory generation, Atropos RL environments, trajectory compression for fine-tuning datasets.

---

## agentskills.io Open Standard

The portability layer for skills across agent systems. Originally developed by Anthropic, released as an open standard.

**Format:**
```
skill-name/
├── SKILL.md          # Required
├── scripts/          # Executable code
├── references/       # Docs loaded on demand  
└── assets/           # Templates, data
```

**SKILL.md frontmatter:**
```yaml
name: skill-name           # 1-64 chars, lowercase+hyphens
description: |             # 1-1024 chars: what + when
  ...
license: MIT
compatibility: [hermes, claude, vscode]
```

**Token budget design (progressive disclosure):**
- Startup: ~100 tokens (metadata only)
- Activation: <5,000 tokens (full instructions)
- On-demand: resources only when needed

**Adoption**: VS Code Copilot, Spring AI, AgentScope Java, Claude API. Cross-ecosystem.

---

## Comparison to This Pipeline's Skill System

| Dimension | Hermes (agentskills.io) | SureThing (this pipeline) |
|-----------|------------------------|---------------------------|
| **Skill creation** | Autonomous after complex tasks | Human-curated, read-only |
| **Skill storage** | Filesystem SKILL.md | `/skills/` in Cell filesystem |
| **Portability** | agentskills.io open standard | Cell-local only |
| **Discovery** | FTS + LLM summarization | Explicit file_read() |
| **Self-improvement** | Skills improve during use | Static until human edits |
| **Security** | Skills Hub quarantine+audit | No marketplace; no external skills |
| **Governance** | None formalized yet | Human-curated = implicit governance |

**The gap on this side**: SureThing's skills don't compound. A complex pipeline task completed at R132 produces no persistent skill document. The knowledge lives in conversation history (ephemeral) and STATE.md (compressed). The agentskills.io pattern suggests a `/skills/pipeline-synthesis/SKILL.md` that would persist the R132 synthesis approach for reuse.

---

## Competitive Position vs. OpenClaw

Hermes is a direct OpenClaw competitor in the self-hosted segment:
- **Hermes**: open-source (MIT), model-agnostic (OpenRouter, 200+ models), self-improving skills, Nous Research pedigree
- **OpenClaw**: commercially-backed (OpenAI-owned), larger ecosystem, deeper protocol support (MCP+A2A), ⚠️ ~20% ClawHub contamination baseline

Facebook AI group post (March 2026): "It can do far more than the Claws and you don't need to buy a Mac Mini."

The arscontexta community is already gravitating toward Hermes for company graph deployment.

---

## ARCHIVIST Project Relevance

Hermes' architecture is directly relevant to the ARCHIVIST harness layer:
- Multi-level memory (session → skills → cross-session search → user modeling) = the memory stack ARCHIVIST needs
- Subagent parallelization via RPC = the execution model for harness layer
- Atropos RL environment = trajectory data for training
- agentskills.io compatibility = portable skill format if ARCHIVIST grows a skill library

**ThunderAgent connection** (from user memory): ThunderAgent is relevant to ARCHIVIST's serving stack — evaluate alongside Hermes for the harness layer architecture.

---

## Security & Governance Notes

**Autonomous skill creation = agent modifying its own behavior.** This is the architectural equivalent of self-modification. Hermes mitigates with Skills Hub quarantine and audit, but:
- No NIST-equivalent standard for autonomous skill creation yet
- This is a Pillar 4 (Security Evaluations) problem that hasn't been addressed
- The `allowed-tools` frontmatter field is the only capability constraint mechanism in the current spec

Monitor for: skill poisoning attacks (analogous to ClawHub malware), drift in autonomous skill quality over time.
