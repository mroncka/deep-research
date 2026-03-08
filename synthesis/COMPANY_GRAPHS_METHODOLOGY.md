# Company Graphs Methodology

**Source:** @arscontexta (Heinrich) — "Company Graphs = Context Repository" (Feb 25, 2026)
**Signal:** 356K impressions, 2.6K bookmarks — high-signal practitioner piece
**Connection:** Directly applicable to `agi-research` pipeline architecture and ARCHIVIST project

---

## Core Thesis

> "Everything is a context problem. When people say AI can't do real work, what they're actually saying is they gave it bad context."

Coding was solved first because the structure was already there — codebases were text files with explicit relationships (imports, calls, types). The agent reads the code, follows the imports, understands the architecture.

Knowledge work doesn't have that structure *yet*. But it can be deliberately engineered.

---

## The Company Graph Architecture

A company graph is a **Git-versioned vault of atomic markdown files connected by wikilinks** that captures the full organizational context:

- Every decision with alternatives and reasoning attached
- Every meeting — not the recording, but extracted claims, decisions, action items, strategic shifts
- Everything published, every research session, every competitive analysis
- Code repositories (the graph concept applies to codebases too)

**Key structural primitives:**
1. **Wikilinks as semantic connections** — explicit edges between nodes
2. **Atomic composable notes** — one claim per note, linkable
3. **Maps of Content (MoC)** — navigation layer for attention management
4. **Metadata for progressive disclosure** — queries + conditional loading
5. **CLAUDE.md** — root context file that teaches the agent how the organization works

---

## Why Markdown Graphs Are Agent-Optimal

The Obsidian/PKM community spent years accidentally engineering the perfect architecture for LLMs:
- Notes that link to each other → traversable graph
- Ideas that are atomic and composable → minimal token waste
- Maps of content → agent attention routing

This is the same structural insight behind agentskills.io's progressive disclosure design:
> Metadata loads at startup (~100 tokens). Full instructions load on activation (<5K tokens). Resources load only when needed.

---

## Tacit Knowledge Capture

The hardest knowledge isn't in documents — it's in people's heads.

When a CTO decides Postgres over Mongo, maybe the decision gets written down. But the reasoning, the tradeoffs considered, the context that made it obvious — that's lost.

**Solution:** Record conversations → agent mines them exhaustively → tacit knowledge becomes structured graph state.

This is not meeting summaries. It's **active synchronization** between a person's thinking and an externalized representation of that thinking.

> "Meetings are how you keep the graph in sync."

---

## Agents as Organizational Memory

Agents live in context windows like humans live in lifespans — temporary, bounded, forget everything when the session ends.

They need externalized knowledge for the same reason we needed writing: to transcend the limits of individual memory.

> "A company graph is an agent's library. Every session it picks up the accumulated knowledge of the entire organization and operates from there."

---

## The Self-Maintaining Graph

The thing that killed every company wiki: maintenance cost. Someone had to keep it updated. Agents don't get bored of maintenance.

An agent operating on a company graph:
- Notices when two notes contradict each other → flags the tension
- Notices when the spec/PRD graph is out of sync with the codebase
- Accumulates friction signals → proposes structural changes to the system itself
- **Refactors its own instructions** → evolves its own architecture when current structure creates drag

---

## Connection to This Pipeline

| Pipeline Component | Company Graph Equivalent |
|-------------------|-------------------------|
| `KNOWLEDGE_GRAPH.md` | `research/` domain knowledge graphs |
| `TOOLS_REGISTRY.md` | `org/competitors/` + `teams/engineering/` |
| `SYSTEMS_THEORY_THREAD.md` | `research/systems-theory/` with wikilinks to `org/decisions/` |
| `pipeline-state.json` | `org/decisions/pipeline-architecture/` with reasoning |
| `CLAUDE.md` (agi-research) | The missing piece — should teach the agent *how* this pipeline works, not just *what* it does |

**The gap:** `agi-research` has the knowledge artifacts but not the graph structure. The files are markdown but they're monolithic blobs, not atomic wikilinked nodes. At current scale (~1.5MB KG) this isn't limiting. At 10MB+ it will be.

**Future direction:** Investigate splitting the KG into atomic node files in `findings/nodes/` with a `findings/MAP_OF_CONTENT.md` navigation layer. The pipeline commits individual node files rather than one monolithic markdown blob.

---

## arscontexta Plugin

Builds the individual graph structure via *semantic metaprogramming* — you describe what you want, the system derives the architecture. Currently in early release with active bug fixing.

Project also building an app: "think Cursor for knowledge work, or networked note-taking apps but rethought AI-native."

**Monitor:** GitHub repo, arscontexta.com, @arscontexta on X.
