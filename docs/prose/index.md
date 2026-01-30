---
layout: docs
title: "PROSE Specification"
display_title: "PROSE: An Architectural Style for AI-Native Development"
permalink: /docs/prose/
nav_order: 1
---

A new discipline is emerging. **AI-Native Development** recognizes natural language as a programming language itself—not a novelty, but a fundamental shift in how we instruct machines.

Just as code became the medium for directing CPUs, natural language is becoming the medium for directing language models. But we are in the infancy of this transition. As an industry, we lack guidance on how to do this *well*—reliably, at scale, for real projects with real complexity.

**PROSE** addresses this gap. It defines an architectural style for reliable, scalable collaboration between humans and AI coding agents. Like REST defined constraints for distributed systems independent of HTTP, PROSE defines constraints for AI-native development independent of any specific model or platform.

---

## Quick Reference

| Constraint | Principle | Induced Property |
|------------|-----------|------------------|
| **P**rogressive Disclosure | Context arrives just-in-time, not just-in-case | Efficient context utilization |
| **R**educed Scope | Match task size to context capacity | Manageable complexity |
| **O**rchestrated Composition | Simple things compose; complex things collapse | Flexibility, reusability |
| **S**coped Boundaries | Autonomy within guardrails | Reliability, security |
| **E**xplicit Hierarchy | Specificity increases as scope narrows | Modularity, inheritance |

---

## What PROSE Is Not

- **Not a framework.** PROSE is a style, like REST. Implementations vary; constraints remain.
- **Not a file format.** The primitives (`.instructions.md`, etc.) are implementations of the style, not the style itself.
- **Not model-specific.** PROSE works with GPT, Claude, Gemini, open-source models, and whatever comes next.
- **Not prescriptive about tooling.** Use VS Code, Cursor, CLI agents, or any interface. The constraints apply universally.

---

## The Problem PROSE Solves

Working with language models at scale reveals a fundamental challenge: **quality in, quality out**—but what does "quality" mean when your programming language is natural language?

Two failure modes dominate:

**Context overload:** Models have finite context and limited attention. When overloaded with irrelevant information, they lose focus, forget instructions, and hallucinate to fill gaps.

**Guidance deficit:** Models given vague, unstructured, or insufficient direction produce inconsistent, unpredictable results. Unlike compilers that reject bad syntax, LLMs *always produce something*—making quality failures silent and insidious.

The industry has prompt engineering techniques for single interactions. But there's no established guidance for AI-assisted development at project scale: How do you provide the right context, at the right time, in the right measure? How do you make interactions *repeatable* and *reliable* across a codebase that evolves?

**PROSE** addresses this through architectural constraints that manage context as a scarce resource, provide structured guidance that scales, bound non-determinism through explicit boundaries, and enable reliable composition of AI capabilities.

---

## The Five Constraints

PROSE defines five architectural constraints. Each addresses a fundamental property of language models and induces desirable system properties.

### P — Progressive Disclosure

> *"Context arrives just-in-time, not just-in-case."*

**Constraint:** Agents receive indexed summaries of available knowledge and capabilities. Full detail is loaded only when the agent determines it is relevant to the current task.

**Rationale:** Context windows are finite. Loading everything upfront wastes capacity and dilutes attention. Progressive disclosure preserves context for what matters.

**Mechanism:** Markdown links as lazy-loading pointers. `SKILL.md` manifests as capability indexes. Hierarchical `AGENTS.md` files as layered context.

**Induced Property:** Efficient context utilization.

---

### R — Reduced Scope

> *"Match task size to context capacity."*

**Constraint:** Complex work is decomposed into tasks sized to fit available context. Each sub-task operates with fresh context and focused scope.

**Rationale:** Attention degrades with context length. When a task exceeds what an agent can hold in focus, quality suffers. Decomposition restores focus.

**Mechanism:** Phased execution (plan → implement → test). Subagent delegation. Session splitting between domains.

**Induced Property:** Manageable complexity, consistent quality.

---

### O — Orchestrated Composition

> *"Simple things compose; complex things collapse."*

**Constraint:** Favor small, chainable primitives over monolithic frameworks. Build complex behaviors by composing simple, well-defined units.

**Rationale:** LLMs reason better with clear, focused instructions. Composition preserves clarity while enabling sophistication. Monolithic prompts become unpredictable.

**Mechanism:** `.instructions.md`, `.prompt.md`, `.agent.md` as atomic primitives. Skills as composable capability packages. Workflows as compositions, not mega-prompts.

**Induced Property:** Flexibility, reusability, maintainability.

---

### S — Scoped Boundaries

> *"Autonomy within guardrails."*

**Constraint:** Every agent operates within explicit boundaries: what tools are available (capability), what context is loaded (knowledge), and what requires human approval (authority).

**Rationale:** LLMs are non-deterministic. Unbounded autonomy produces unpredictable results. Boundaries constrain variance while preserving usefulness.

**Mechanism:** Tool whitelists. `applyTo` patterns for context scoping. Validation gates requiring human approval. Deterministic tools (MCP) as anchors.

**Induced Property:** Reliability, trust, safety.

*This constraint is foundational to agentic security—agents that operate within explicit boundaries are auditable, controllable, and safer.*

---

### E — Explicit Hierarchy

> *"Specificity increases as scope narrows."*

**Constraint:** Instructions form a hierarchy from global to local. Local context inherits from and may override global context. Agents resolve context by walking up the hierarchy.

**Rationale:** Different domains require different guidance. Global rules ensure consistency; local rules enable specialization. Hierarchy prevents context pollution.

**Mechanism:** Root `AGENTS.md` defines project-wide principles. Nested `AGENTS.md` files add domain-specific rules. `.instructions.md` with `applyTo` patterns enable file-type targeting.

**Induced Property:** Modularity, domain adaptation, inheritance.

---

## How Constraints Relate

The five constraints form an integrated system:

- **Progressive Disclosure** determines *what* enters context
- **Reduced Scope** determines *how much* the agent handles at once
- **Orchestrated Composition** determines *how primitives combine*
- **Scoped Boundaries** determine *what the agent can do*
- **Explicit Hierarchy** determines *which rules apply*

---

## Grounding Principles

PROSE stands on three foundational truths about language models:

### 1. Context is finite and fragile

Context windows have capacity limits, and attention within those limits is not uniform. Information competes for attention; content far from focus gets lost. Treat context as a scarce resource that degrades under load.

*Implication: Manage both quantity and quality of what enters the window.*

### 2. Context must be explicit

Agents can only work with externalized knowledge. Tacit understanding, undocumented decisions, implicit agreements, and prior session history are invisible to AI. Models are stateless—what isn't in the context window doesn't exist for the agent.

*Implication: Continuously surface and codify the knowledge your projects depend on.*

### 3. Output is probabilistic

The same input can produce different outputs. Language models interpret rather than execute; variance is inherent. Determinism comes from constraints, structure, and grounding—not from the model itself.

*Implication: Reliability is architected through boundaries and guardrails, not assumed.*

These properties persist regardless of model size, architecture, or provider.

---

## PROSE Compliance Checklist

Assess whether your AI-native development approach is PROSE-compliant:

| Constraint | Compliance Question | ✓ |
|------------|---------------------|---|
| **Progressive Disclosure** | Is context loaded on-demand rather than all upfront? Do agents see indexes/summaries before full detail? | |
| **Reduced Scope** | Are complex tasks decomposed into right-sized subtasks? Do agents get fresh context per phase? | |
| **Orchestrated Composition** | Are capabilities built from small, chainable primitives? Or do you rely on monolithic mega-prompts? | |
| **Scoped Boundaries** | Are agent capabilities, knowledge scope, and approval requirements explicitly defined? | |
| **Explicit Hierarchy** | Do instructions form a global-to-local hierarchy? Can local rules specialize or override global ones? | |

**Scoring:**
- **5/5:** Fully PROSE-compliant
- **3-4/5:** Partially compliant—identify gaps and address
- **0-2/5:** Ad-hoc approach—significant restructuring needed

---

## PROSE Maturity Model

The journey from ad-hoc prompting to PROSE-compliant systems:

| Level | Name | Description | Key Indicators |
|-------|------|-------------|----------------|
| **0** | **Ad-hoc** | One-off prompts with no persistent context or structure | No saved instructions; each session starts fresh; results vary wildly |
| **1** | **Structured** | Persistent instructions guide agent behavior | `.instructions.md` or `AGENTS.md` in use; some repeatability emerges |
| **2** | **Composed** | Multiple primitives work together with explicit boundaries | Skills, workflows, and hierarchical context; validation gates; clear scoping |
| **3** | **Orchestrated** | Multi-agent coordination with fresh context per scope | Subagent delegation; session splitting; async agent workflows; continuous context capture |
| **4** | **Distributed** | Primitives packaged and reused across projects and teams | Skills published as packages; cross-project primitive consumption; ecosystem participation |

### Level Progression

- **0 → 1:** Recognize that instructions should persist beyond a single session
- **1 → 2:** Recognize that primitives compose; structure enables reliability
- **2 → 3:** Recognize that complex work requires coordination across agents and phases
- **3 → 4:** Recognize that well-structured primitives are inherently shareable—the "npm moment"

**Level 4 insight:** PROSE constraints don't just improve your project—they make your primitives *distributable*. Quality structure enables ecosystem reuse. This is when AI-native development scales beyond individual teams to community-level compound intelligence.

---

## Anti-Patterns

Clear examples of what violates PROSE:

| Anti-Pattern | Violated Constraint | Why It Fails |
|--------------|---------------------|--------------|
| **Mega-prompt** | Orchestrated Composition | Monolithic instructions become unpredictable; too much competes for attention |
| **Context dumping** | Progressive Disclosure | Wastes context capacity; dilutes attention on what matters |
| **Undocumented rules** | Grounding Principle #2 | Agents can only use explicit context; invisible rules produce invisible failures |
| **Unbounded agent** | Scoped Boundaries | Unbounded autonomy + non-determinism = unpredictable and unsafe behavior |
| **Flat instructions** | Explicit Hierarchy | No specialization possible; either over-general or polluted with irrelevant detail |
| **Stale context** | Grounding Principle #2 | Context must be explicit *and current*; stale guidance produces stale results |
| **Scope creep** | Reduced Scope | Attention degrades; quality suffers; agent loses track of earlier instructions |

**The meta-pattern:** Most anti-patterns violate the principle that *context is finite and fragile*.

---

## The Outcomes

When PROSE constraints are followed, systems exhibit:

| Outcome | Description |
|---------|-------------|
| **Reliability** | Consistent results from non-deterministic systems |
| **Scalability** | Same patterns work from simple scripts to large, complex codebases |
| **Portability** | Works across any LLM-based agent platform |
| **Maintainability** | Primitives can evolve independently |
| **Transparency** | Agent behavior is inspectable and explainable |
| **Security** | Explicit boundaries and inspectable behavior reduce attack surface and enable audit |

---

## Summary

**PROSE** is an architectural style for AI-native development defined by five constraints:

| Constraint | Core Idea |
|------------|-----------|
| **P**rogressive Disclosure | Load context just-in-time |
| **R**educed Scope | Right-size tasks to context capacity |
| **O**rchestrated Composition | Compose simple primitives |
| **S**coped Boundaries | Bound autonomy with explicit limits |
| **E**xplicit Hierarchy | Layer guidance from global to local |

When followed, these constraints induce reliability, scalability, and portability in AI-assisted development—independent of any specific model, platform, or technology.

---

**Ready to implement PROSE?** Continue to [Core Concepts](../concepts/) for practical patterns, or jump to [Getting Started](../getting-started/) for hands-on implementation.
