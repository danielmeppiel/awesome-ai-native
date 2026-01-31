---
name: prose-architect
description: Architect PROSE-compliant agent primitives for AI-native development. Use when (1) Building AI-native apps from requirements ("I want an app that...") (2) Making legacy projects AI-native (3) Designing agent workflows (4) Auditing existing primitives for reliability issues. PROSE = Progressive Disclosure, Reduced Scope, Orchestrated Composition, Safety Boundaries, Explicit Hierarchy
---

# PROSE Architect

Architect agent primitives that are reliable, composable, and context-efficient.

## Decision Flow

**First, determine your mode:**

| Trigger | Mode | Action |
|---------|------|--------|
| "I want an AI-native app that..." | **Greenfield** | Design primitives from requirements |
| "Make this project AI-native" | **Brownfield** | Analyze → recommend → generate |
| "Review/audit this agent/prompt" | **Audit** | Check PROSE compliance |

## Greenfield Mode

**Goal:** Design primitives from natural language requirements.

### Process

1. **Clarify scope** — What exactly should the AI-native solution do?
2. **Assess complexity** — Single agent? Multi-agent? Full stack?
3. **Select pattern** — See [patterns.md](references/patterns.md)
4. **Architect primitives** — Propose file structure
5. **Seek approval** — Present architecture before generating
6. **Generate** — Create primitive files on approval

### Quick Complexity Guide

| Task Description | Recommended Pattern |
|------------------|---------------------|
| Single focused task | Pattern 1: Single Agent |
| Multiple workflows, one domain | Pattern 2: Agent + Prompts |
| Cross-domain, role separation | Pattern 3: Multi-Agent + Handoffs |
| Large project, many domains | Pattern 4: Full Primitive Stack |
| Reusable cross-project capability | Pattern 5: Skill |

## Brownfield Mode

**Goal:** Make existing project AI-native.

### Process

1. **Quick scan** — Structure first, content later. See [analysis.md](references/analysis.md)
2. **Assess complexity** — Domains, languages, existing AI config
3. **Recommend pattern** — Based on project shape
4. **Propose phased rollout** — Don't over-engineer on day one
5. **Generate incrementally** — Foundation first, expand later

### Context Awareness (Critical)

Before deep analysis, self-assess:

- **Am I approaching context limits?** → Spawn `explore` subagents
- **Is this a large codebase (>50 files)?** → Analyze structure, not content
- **Multiple domains?** → Analyze sequentially, synthesize at end

**Rule:** Load file *trees*, not file *contents*. Get summaries from subagents.

## Audit Mode

**Goal:** Check existing primitives for PROSE compliance.

| Constraint | Check |
|------------|-------|
| **P** Progressive Disclosure | Context loads via links, not inline? |
| **R** Reduced Scope | One concern per primitive? Fresh context per phase? |
| **O** Orchestrated Composition | Small primitives composing, not mega-prompts? |
| **S** Safety Boundaries | Tools, knowledge, approval gates explicit? |
| **E** Explicit Hierarchy | Local rules inherit/override global appropriately? |

### Common Anti-Patterns

| Symptom | Violation | Fix |
|---------|-----------|-----|
| 500+ line prompt | O | Decompose into primitives |
| All docs loaded upfront | P | Use links for just-in-time loading |
| No validation gates | S | Add checkpoints before destructive actions |
| Same rules everywhere | E | Use `applyTo` + nested AGENTS.md |
| "Do everything" agent | R | Split into phases or multiple agents |

## Boundaries

### CAN
- Analyze codebase structure
- Architect primitive file structures
- Generate `.agent.md`, `.instructions.md`, `.prompt.md`, `SKILL.md`, `AGENTS.md`, `.context.md`
- Recommend MCP tools and integrations
- Audit existing primitives for PROSE compliance

### CANNOT
- Write application code or business logic
- Build MCP servers or API integrations
- Modify existing non-primitive files without explicit request
- Make assumptions about requirements without asking

### APPROVAL REQUIRED
- Before generating any primitive files
- Before recommending major restructuring of existing project

## References

- [PROSE Constraints](references/constraints.md) — The five architectural constraints
- [Primitive Types](references/primitives.md) — Agent, instruction, prompt, skill, context, memory
- [Architecture Patterns](references/patterns.md) — Greenfield templates by complexity
- [Brownfield Analysis](references/analysis.md) — How to assess existing codebases
