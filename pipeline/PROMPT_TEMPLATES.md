# Prompt Templates

LLM prompt templates for synthesis steps. All templates use `{{placeholder}}` syntax.

---

## Template 1: Delta Extraction

```
You are a research synthesis engine for an AGI intelligence pipeline.

Current living knowledge base (abbreviated):
{{KNOWLEDGE_GRAPH_SUMMARY}}

Raw research sweep results:
{{WEB_RESEARCH_SUMMARIES}}

Extract ONLY findings that:
1. Do not already exist in the knowledge base above
2. Are structurally significant (change the model, not just update a detail)
3. Are actionable or predictive

For each delta, output:
- CLASS: [CAPABILITY_LEAP | FRAMEWORK_CHANGE | SECURITY_EVENT | GOVERNANCE_MILESTONE | HARDWARE_INFLECTION | EMERGENCE_SIGNAL | MARKET_STRUCTURE]
- FACT: What happened (one sentence, primary source if available)
- IMPLICATION: What this changes about the current model
- PREDICTION: What this implies for next 30-90 days
- CONFIDENCE: [CONFIRMED | CORROBORATED | REPORTED | INFERRED]
- SUBSTRATES: Which of [KG, TOOLS, SYSTEMS] need updating

Output as structured list. If no genuine deltas exist, output: DELTAS: NONE
```

---

## Template 2: KG Node Generation

```
Given this delta:
{{DELTA}}

And the current KG node schema:
{{KG_NODE_SCHEMA}}

Generate the KG update:
1. New nodes (if any): type, name, required fields
2. New edges (if any): source → edge_type → target
3. Updated nodes (if any): node_name, field, old_value → new_value

Use ONLY node types and edge types defined in the schema.
Mark confidence tier on each node/edge.
```

---

## Template 3: Tools Registry Entry

```
Given this delta about a tool/framework:
{{DELTA}}

Generate a tools registry entry using this schema:
### [Tool Name] vX.Y.Z
- Category: [orchestration|runtime|model|protocol|hardware|security]
- Status: [active|maintenance|deprecated|experimental]
- Stack Fit: [PRODUCTION-READY|STAGING-READY|EXPERIMENTAL|MAINTENANCE-ONLY|DEPRECATED]
- Cost Model: [assessment]
- Security Posture: [CLEAN|PATCHED|ACTIVE-VULNS|CRITICAL|UNKNOWN]
- Protocol Support: MCP [✅/❌] | A2A [✅/❌] | AG-UI [✅/❌]
- Benchmark: [if available]
- Notes: [structurally significant points only]
```

---

## Template 4: Systems Theory Correlation

```
Given this delta:
{{DELTA}}

And these active thesis threads:
{{ACTIVE_THESES}}

Does this delta:
a) Confirm, extend, or contradict an existing thesis thread? → Update existing entry
b) Represent a new systemic pattern not covered by existing threads? → Create new entry
c) Neither — purely tactical finding with no systemic implication? → Skip

If (a) or (b), generate a systems thread correlation entry:
### [Run NNN] — [Phenomenon Name]
- Signal Source: [delta reference]
- Systems Pattern: [emergence|phase_transition|power_law|self_organization|cascade|attractor|bifurcation]
- Mechanism: [proposed causal mechanism — be specific]
- Evidence Grade: [CONFIRMED|INFERRED|HYPOTHETICAL]
- Quantification: [if applicable]
- Prediction: [specific, testable, time-bounded]
- Connects To: [prior thread entry if applicable]
```

---

## Template 5: Run Report

```
Generate a run report for AGI Research Pipeline Run {{RUN_NUM}}.

Run metadata:
- Timestamp: {{TIMESTAMP}}
- Previous SHA: {{PREV_SHA}}
- Tracks swept: A (AGI), B (Agentic), C (Security), D (Systems), E (Governance), F (Hardware)

Deltas found:
{{DELTAS}}

Report format:
# AGI Research — Run {{RUN_NUM}}
**{{TIMESTAMP}}** | prev: {{PREV_SHA}}

## Key Findings
[3-5 sentence narrative of the most significant deltas — what changed, what it means, what to watch]

## Deltas
[Structured list of all deltas with CLASS, FACT, IMPLICATION, PREDICTION]

## Artifact Updates
- KG: [N] new nodes, [M] new edges
- Tools: [N] entries updated
- Systems: [N] correlations added

## Next Run Watch List
[2-3 specific things to watch for in the next 30-60 minutes based on current signals]
```
