# PROSE Constraints

Five architectural constraints for reliable AI-native development.

## P — Progressive Disclosure

> *"Context arrives just-in-time, not just-in-case."*

**Constraint:** Load context only when relevant. Use summaries/indexes; fetch detail on demand.

**Mechanism:**
- Markdown links as lazy-loading: `[spec](./spec.md)`
- SKILL.md descriptions as capability indexes
- Hierarchical AGENTS.md as layered context

**Violation:** Loading entire codebase into every session.

---

## R — Reduced Scope

> *"Match task size to context capacity."*

**Constraint:** Decompose work into tasks that fit available context. Fresh context per phase.

**Mechanism:**
- Phased execution: plan → implement → test
- Subagent delegation for isolated concerns
- Session splitting between domains

**Violation:** Single agent handling 10-step complex workflow in one session.

---

## O — Orchestrated Composition

> *"Simple things compose; complex things collapse."*

**Constraint:** Build from small, chainable primitives. No monolithic mega-prompts.

**Mechanism:**
- `.instructions.md`, `.prompt.md`, `.agent.md` as atoms
- Skills as composable packages
- Workflows as compositions

**Violation:** 500-line prompt with all instructions, rules, and context inline.

---

## S — Scoped Boundaries

> *"Autonomy within guardrails."*

**Constraint:** Explicit limits on tools, knowledge, and authority. Human approval at gates.

**Mechanism:**
- Tool whitelists in agent definitions
- `applyTo` patterns for context scoping
- Validation gates: "Seek approval before..."
- MCP tools as deterministic anchors

**Violation:** Agent with access to all tools and no approval checkpoints.

---

## E — Explicit Hierarchy

> *"Specificity increases as scope narrows."*

**Constraint:** Global rules inherited by local. Local can specialize or override.

**Mechanism:**
- Root `AGENTS.md` for project principles
- Nested `AGENTS.md` for domain rules
- `.instructions.md` with `applyTo` for file-type targeting

**Violation:** Flat instructions with no inheritance; same rules for frontend and backend.

---

## Grounding Principles

These constraints rest on three truths about LLMs:

1. **Context is finite and fragile** — Attention degrades with length. Treat context as scarce.
2. **Context must be explicit** — Tacit knowledge is invisible. Externalize everything.
3. **Output is probabilistic** — Same input, different outputs. Reliability is architected, not assumed.
